---
updated: 2026-06-12 10:30
project: hermes-external-access
branch: HEAD (main)
---

## 작업 요약: hermes dashboard 외부 접속 설정 및 검증

### 완료된 단계
- [x] Caddyfile에 access log 블록 추가 (`/opt/web-infra/Caddyfile`, 9119/443 모두)
- [x] docker-compose.yml에 로그 볼륨 마운트 추가 (`./caddy/logs:/var/log/caddy`)
- [x] Caddy 컨테이너 재시작 및 inode 재바인딩 (`docker compose up -d --force-recreate`)
- [x] caddy-ufw-watch.service 설치 및 활성화 (Caddy 재시작 시 ufw-docker 규칙 자동 재적용)
- [x] apply-ufw.sh에 9119/tcp 허용 + hermes-dnat 재시작 추가
- [x] UFW 상태 확인: 9119/tcp ALLOW IN Anywhere, ALLOW FWD 172.18.0.4:9119
- [x] DNS 확인: snowball.me.kr → 221.165.64.216 (A 레코드 정상)
- [x] cloudflared 설치 (사용자가 직접: `curl ... -o /tmp/cloudflared`)
- [x] Cloudflare Quick Tunnel 외부 접속 확인: `https://shine-seal-advantage-bugs.trycloudflare.com` → Hermes Agent - Dashboard ✅

### 미완료: 핵심 차단 사항
- [ ] **`snowball.me.kr:9119` 직접 외부 접속** — KT 가정용 ISP/라우터 인바운드 차단 중
  - WebFetch에서 443, 9119 모두 60초 타임아웃
  - Caddy 로그에 `remote_ip: 172.18.0.1`(내부)만, 외부 IP 없음

### 다음 단계

**방법 A: KT 라우터 방화벽 설정 변경** (근본 해결)
1. `http://172.30.1.254:8899/login` 접속
2. 보안 > 방화벽 수준 → `낮음` 변경 (또는 인바운드 허용 규칙에 9119 추가)
3. 포트포워딩 9119 활성 상태 확인 (체크 표시 확인)
4. 저장 후 라우터 재부팅
5. 모바일 LTE에서 `https://snowball.me.kr:9119/` 접속 테스트
6. 서버에서 `tail -f /opt/web-infra/caddy/logs/access-9119.log` 확인

**방법 B: Cloudflare Named Tunnel** (KT 차단 영구 우회)
- cloudflared가 `/tmp/cloudflared`에 설치됨
- Cloudflare 계정 필요: `cloudflared tunnel login`
- `sudo mv /tmp/cloudflared /usr/local/bin/cloudflared` (root 권한)
- Named Tunnel 설정 후 snowball.me.kr DNS를 Cloudflare 경유로 변경

### 인계 노트
- **KT 가정용 ISP는 인바운드 차단**: 포트포워딩이 설정돼도 ISP/라우터 방화벽이 차단 중
- **서버 자체 설정은 완벽**: Caddy, UFW, docker-proxy 모두 정상
- **hairpin NAT 없음**: 서버(172.30.1.92)에서 221.165.64.216:9119로 테스트 불가
- **cloudflared 위치**: `/tmp/cloudflared` (재부팅 시 사라짐, 영구 설치 필요시 `sudo mv`)
- **Cloudflare Quick Tunnel은 임시 URL** — 세션마다 URL 변경됨, 검증용으로만 사용
- **stop hook 요구사항**: `snowball.me.kr:9119` 직접 접속 시 Caddy 로그에 외부 IP 등장 필요
