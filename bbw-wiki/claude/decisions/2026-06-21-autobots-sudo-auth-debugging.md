---
title: Autobots 봇 자율 sudo + 승인 UI — 인증 다이얼로그/카드 디버깅 기록
date: 2026-06-21
tags: [autobots, caddy, basic-auth, safari, fastify, sse, troubleshooting, decision]
---

# Autobots 봇 자율 sudo: 인증 다이얼로그 & 승인 카드 디버깅

## 배경
봇이 작업 중 필요한 sudo를 자율 실행(자동허용 4종) / 위험명령은 승인 게이트로 처리하는 기능 구현.
컨테이너 배포라 **컨테이너 봇 → 백엔드 큐 → 호스트 root executor 데몬** 모델 채택. 이후 승인 UI(사이드바 + 채팅 인라인)를 붙이는 과정에서 **두 증상이 끈질기게 재발**: (1) 사이드바/채팅 이동 시 로그인 다이얼로그, (2) 승인 카드 미표시. 여러 라운드 디버깅 끝에 근본원인 3개를 규명.

## 근본원인 & 해결

### 1. Fastify SSE 크래시 루프 (카드 미표시·불안정의 숨은 원인)
- `plugins/sse.ts`의 `/events`가 `reply.hijack()`를 **맨 끝**에 호출 + SSE 클라이언트 한도 초과 시 hijack 없이 return → Fastify onSend 훅이 헤더 재기록 → `ERR_HTTP_HEADERS_SENT` → **Node 프로세스 사망 → 컨테이너 RestartCount 13 재시작 루프**.
- 프론트에서 `/events` EventSource를 roster 변경마다 여닫아 한도 초과를 유발해 노출.
- **해결**: `/events` 핸들러 **진입 즉시 `reply.hijack()`** 호출. 프론트 EventSource는 ref로 마운트 1회만 연결.

### 2. Caddy basic_auth + Safari → 매 네비게이션 로그인 다이얼로그 (핵심)
- **Safari는 fetch/XHR엔 basic-auth 자격증명을 보내지만 top-level 문서 네비게이션(`Sec-Fetch-Mode: navigate`)엔 보내지 않는다** → 문서 401 → 로그인 다이얼로그. (Caddy access log에서 `mode=navigate, Authorization 없음, status 401`로 확정.)
- 추가로 PWA `manifest.json`·`_next/*` 청크·RSC `*.txt`는 브라우저가 자격증명 없이 가져와 401 → 다이얼로그. (다이얼로그를 띄우는 건 **리소스/문서 로드 401**이지 fetch 401이 아님.)
- **해결 (Caddyfile, /opt/web-infra)**:
  - `@public path /manifest.json /_next/* *.txt /favicon.ico /icon-*.png ...` → basic_auth 제외(비민감).
  - **세션 쿠키 보조 인증**: basic_auth 통과 시 `header +Set-Cookie "autobots_sess=<token>; Path=/autobots; HttpOnly; Secure; SameSite=Lax"` → `@hassess header Cookie *autobots_sess=<token>*` 매처로 이후 요청 basic_auth 생략. 브라우저는 쿠키를 네비게이션에 안정 전송 → **다이얼로그 최초 1회만**. 보안: basic_auth와 동등(통과 후에만 발급, HttpOnly/Secure).

### 3. 검증 방식 (디버깅 장기화의 진짜 교훈)
서버측 curl만으로 "고쳤다"며 매번 사용자 브라우저 테스트에 의존 → "아직도 그대로" 반복. 실제론 크래시 루프/스테일 컨테이너로 변경이 도달 못 한 라운드도 있었음.
- **자율 e2e 검증 확립**: Playwright(전역 설치) 헤드리스 + 발급한 **세션 쿠키를 `addCookies`로 주입**해 basic_auth 우회(비밀번호 불필요) + `--host-resolver-rules=MAP snowball.me.kr 127.0.0.1`. → 네비게이션 401=0·다이얼로그 0회·카드 렌더(`sudo 권한 승인 필요` 검출) 직접 확인.

## 결정 (재발 방지 규칙)
1. **SPA + Caddy basic_auth는 세션 쿠키 보조 + 정적/RSC public 제외를 기본 패턴으로.** 순수 basic_auth만으론 Safari에서 네비게이션마다 다이얼로그 발생.
2. **SSE/스트리밍 Fastify 핸들러는 진입 즉시 hijack.**
3. **Docker 백엔드 변경은 항상 `build && up -d`** (소스가 이미지에 구워짐).
4. **브라우저측 이슈는 헤드리스+쿠키 주입으로 자율 검증** 후 보고. Caddy access log의 `Sec-Fetch-Dest`/`Authorization`로 다이얼로그 유발 요청 특정.

## 후속 실패 (같은 날) — 승인/거부 버튼 미작동

**증상**: 채팅 인라인 카드의 거부 버튼을 눌러도 백엔드 미반영(요청 계속 pending), 대화 전환 후 복귀하면 카드 재등장.

**근본원인 (2겹)**:
1. Caddy `header_up X-Admin-Secret {env.AUTOBOTS_ADMIN_SECRET}`(및 `{$VAR}`)가 **이 배포에서 빈 값으로 주입** → 백엔드 `requireAdmin` 401 → approve/deny 전부 실패. 백엔드 임시 디버그 로깅(`givenLen=0 expLen=44`)으로 확정. (시크릿 일치·`caddy adapt` 치환·백엔드 직접호출 200까지 정상으로 보여 오래 헤맴 — 수신측 로깅이 결정타.)
2. 프론트 `actSudo`가 `res.ok` 확인 없이 **낙관적으로 카드 제거** → 401이어도 사라져 "처리된 듯" 보이고, 재조회 시 pending이라 재등장.

**해결**: 
- approve/deny 인가를 **시크릿 헤더 → 네트워크 출처 게이트**로 전환. 사람=리버스 프록시 경유(사설 비-루프백) 허용, 봇=컨테이너 내부 localhost(루프백) 차단 → 자가승인 방지. 시크릿 주입 의존 제거.
- 프론트 `actSudo`: `res.ok`일 때만 카드 제거, 실패 시 서버 재동기화.
- Caddy의 X-Admin-Secret 주입 제거(쿠키 인증·정적 public 제외는 유지).
- 검증: Playwright 헤드리스로 거부 버튼 클릭 → DB `denied(decided_by=user)` + 대화 전환 복귀 후 카드 미재등장 확인.

**추가 결정**: 프록시 env placeholder로 upstream 헤더에 시크릿 주입 금지(불안정). 인가는 네트워크 경로/명시 토큰으로. 상태변경 UI는 `res.ok` 필수.

## 관련 파일
- 백엔드: `autobots/backend/{services/sudo-policy.ts, routes/sudo.ts, lib/bot-spawn.ts, plugins/sse.ts, routes/nav.ts}`
- 스크립트: `autobots/scripts/bot-sudo/{sudo-executor,botsudo,install-bot-sudo.sh}`, `autobots/scripts/apply-caddy-session-cookie.sh`
- 인프라: `/opt/web-infra/Caddyfile`, `autobots/docker-compose.yml`
- 로컬 메모리: `lessons.md` 2026-06-21, `bot-autonomous-sudo.md`
