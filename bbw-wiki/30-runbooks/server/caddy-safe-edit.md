---
title: "라이브 Caddyfile 안전 편집 절차 (in-place 편집 금지)"
type: runbook
summary: "라이브 /opt/web-infra/Caddyfile 을 in-place 편집하다 0바이트로 날린 사고(2026-06-28)와, 후보-검증-승격 안전 절차. 모든 인프라 config 라이브 편집에 적용."
tags: [infra, caddy, runbook, incident, devops, stellina]
created: 2026-06-28
updated: 2026-06-28
status: ai-curated
---

# 라이브 Caddyfile 안전 편집 절차

> 사고 기반 런북 | 대상: `/opt/web-infra/Caddyfile`(전 도메인 라우팅·인증) 및 모든 라이브 config 파일. 담당: 스텔리나(DevOps/인프라).

## 실패 사례 (2026-06-28) — 원인

`console.snowball.me.kr` 블록을 mTLS → basic_auth 로 바꾸는 작업 중, 라이브 `/opt/web-infra/Caddyfile` 을 **in-place 로 직접 편집**하다 `tee`/`cp`/`>` 가 오작동해 **파일이 0바이트로 비워짐**. 함께 만든 백업(`Caddyfile.new`, `Caddyfile.bak-console-*`)도 truncate 이후/빈 입력으로 만들어져 **모두 0바이트** — 백업도 무용.

- **영향**: web_caddy 가 마침 리로드되지 않아(Up 상태로 옛 설정 메모리 보존) 사이트는 유지됐으나, **리로드/재시작 시 전 도메인 라우팅·인증 소실**이 되는 near-outage 잠재 폭탄이었다.
- **근본 원인**: ①라이브 파일 직접 편집 ②검증 없이 적용 시도 ③백업을 변경 *이후* 또는 빈 내용으로 생성(비어있지 않음을 확인 안 함).

## 성공 절차 (복구 시 실제로 통한 방법) — 반드시 이대로

라이브 파일을 **절대 직접 편집하지 말고**, 후보 → 검증 → 승격 순서로:

```bash
# 1) 최신 '비어있지 않은' 정상본을 후보로 복사 (크기 확인 필수)
ls -la /opt/web-infra/Caddyfile.bak-*          # 최신 + 3KB대 = 정상본 선택
cp /opt/web-infra/Caddyfile.bak-<최신정상> /opt/web-infra/caddy/config/Caddyfile.candidate

# 2) 후보에서만 대상 블록 수정 (라이브 미접촉). 수정 후 정상본과 diff 로 의도한 변경만 됐는지 확인
diff /opt/web-infra/Caddyfile.bak-<최신정상> /opt/web-infra/caddy/config/Caddyfile.candidate

# 3) 컨테이너로 구문 검증 — config 디렉터리는 /config 로 마운트됨
docker exec web_caddy caddy validate --adapter caddyfile --config /config/Caddyfile.candidate
#   → "Valid configuration" 안 나오면 여기서 중단(라이브 안전)

# 4) 검증 통과 시에만 라이브로 승격 + 리로드
cp /opt/web-infra/caddy/config/Caddyfile.candidate /opt/web-infra/Caddyfile
docker exec web_caddy caddy reload --config /etc/caddy/Caddyfile
#   reload 가 안 먹으면(이력 있음): docker restart web_caddy

# 5) 적용 후 라우팅 검증 — 외부 DNS 대신 호스트 caddy 에 --resolve 로 직접
curl -sk --resolve console.snowball.me.kr:443:127.0.0.1 -o /dev/null -w "%{http_code}\n" https://console.snowball.me.kr/   # 401=basic_auth OK
curl -sk --resolve snowball.me.kr:443:127.0.0.1 -o /dev/null -w "%{http_code}\n" https://snowball.me.kr/autobots/          # 401/200=정상
```

## 체크리스트 (요약)
- [ ] 라이브 파일 **직접 편집 금지** — 후보 파일에서만 작업
- [ ] 변경 전 백업이 **비어있지 않은지**(`wc -c`) 확인
- [ ] `caddy validate` **통과 후에만** 라이브 승격
- [ ] `diff` 로 의도한 블록만 바뀌었는지 확인(시크릿/쿠키/다른 라우트 보존)
- [ ] 적용 후 `curl --resolve` 로 401/200 라우팅 검증
- [ ] 마운트는 **파일 바인드**(`/opt/web-infra/Caddyfile`→`/etc/caddy/Caddyfile`)라 후보는 디렉터리 마운트(`caddy/config`→`/config`)에 둬야 컨테이너가 봄

## 관련
- 콘솔 mTLS 배포 맥락: [[live-console-caddy-mtls-deploy]]
- 인증 구조: [[autobots-auth-security]]
- 유실 방지 원칙: [[rollback-prevention]]
