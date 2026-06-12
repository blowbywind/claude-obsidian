# web-infra

## 핵심
홈서버 Docker 인프라. 도메인: snowball.me.kr / 서버 IP: 221.165.64.216

⚠️ **주의**: rm -rf 명령어 실행 전 반드시 현재 상태 확인 (2026-06-08 /opt/web-infra 전체 삭제 사고)
⚠️ **주의**: 새 컨테이너 외부 노출 시 `sudo ufw-docker allow <container> <port>/tcp` 필수
⚠️ **주의**: `docker compose up/down` 또는 `ufw reset` 후 외부 접속 타임아웃 시 → `sudo /opt/web-infra/apply-ufw.sh` 실행

## 현재 상태
- 위치: `/opt/web-infra`
- 서비스: caddy (80/443/9119), hermes-dashboard (19119 내부), postgres (내부), adminer (127.0.0.1:8080), seaweedfs (내부)
- DB: PostgreSQL 16 / user: bbw / db: bbw_db
- git 관리 중 (docker-compose.yml, Caddyfile, backup.sh)
- 백업: 매일 03:00 systemd timer → `/mnt/storage/backups/`
- **hermes 외부 접속**: `https://snowball.me.kr:9119/` ✅ (2026-06-12 확인)

## 자동 복구 설정

| 스크립트/서비스 | 역할 |
|---|---|
| `sudo /opt/web-infra/apply-ufw.sh` | 수동 복구 (브리지 정리 + ufw-docker + hermes-dnat) |
| `caddy-ufw-watch.service` (root) | web_caddy start 이벤트 → ufw-docker 자동 재적용 |

**설치 명령** (최초 1회):
```bash
sudo cp /opt/web-infra/caddy-ufw-watch.service /etc/systemd/system/
sudo systemctl enable --now caddy-ufw-watch.service
```

**외부 접속 불가 체크리스트**:
1. `timeout` 응답 → UFW 차단 → `sudo /opt/web-infra/apply-ufw.sh`
2. `connection refused` → 서비스 미실행 → `docker ps`, `systemctl --user status hermes-dashboard`
3. `SSL error` → Caddy 인증서 문제 → `docker logs web_caddy`

## 아키텍처 결정
- **ufw-docker** (2026-06-08): UFW + Docker 충돌 해결. ufw reload 이제 안전.
- **postgres expose** (2026-06-08): ports → expose로 변경. 외부 바인딩 제거.
- **/opt 위치** (2026-06-08): 서비스를 /home에서 /opt로 이전. 사용자 계정 종속 제거.
- **Caddy 인증서**: staging CA로 오염된 적 있음 → 문제 시 caddy/data 초기화 후 재시작.

## 디스크 구성
- `/` (NVMe LVM): 455GB, 현재 ~15GB 사용
- `/mnt/storage` (sda ext4): 110GB, 백업/대용량 파일 전용

## 주의사항
- `ufw reload` 이전에는 Docker 규칙 소멸 위험 → ufw-docker 설치 후 해결됨
- `docker compose up/down` 시 포트 노출 서비스는 트래픽 적은 시간에
- 대용량 파일 전송은 서버에서 직접 (로컬 업로드 금지)

## hermes 외부 접속 (2026-06-12 완료)

**접속 URL**: `https://snowball.me.kr:9119/`

**증거**: Caddy `access-9119.log`에 `remote_ip: 172.30.1.254` (KT 라우터 IP) 2회 세션
- [07:51] 완전 페이지 로드 + WebSocket 터미널(`/api/pty`) 연결
- [20:27] 재접속 + WebSocket 터미널 연결

**동작 원리**: KT GiGA WiFi Home 라우터의 **hairpin NAT**
- LAN 기기 → `snowball.me.kr:9119` (DNS: 221.165.64.216) → 라우터 포트포워딩 → 서버(172.30.1.92:9119) → docker-proxy → Caddy → hermes
- 라우터가 source IP를 자신의 LAN IP(172.30.1.254)로 SNAT → Caddy에 172.30.1.254로 기록

**⚠️ 테스트 시 주의**: 서버(172.30.1.92) 자체에서 221.165.64.216:9119 접속 테스트는 항상 실패 (hairpin 불가). 반드시 다른 LAN 기기(노트북, 폰)에서 테스트.

**최종 Caddyfile 핵심 설정**:
```caddyfile
{
    servers {
        trusted_proxies static 127.0.0.1 172.18.0.0/16
    }
}
snowball.me.kr:9119 {
    log { output file /var/log/caddy/access-9119.log; format json }
    reverse_proxy hermes-dashboard:19119
}
```

---

## 작업 히스토리
- 2026-06-12: hermes 외부 접속 완료 — trusted_proxies·access log 볼륨·9119 포트 전체 구성. Caddy remote_ip: 172.30.1.254 확인.
- 2026-06-11: 자동 복구 인프라 추가 (caddy-ufw-watch.service, apply-ufw.sh) — 컨테이너 재시작 시 ufw-docker 규칙 만료 이슈 영구 해결
- 2026-06-08: ufw-docker 설치, postgres 보안 강화, /opt 이전, 디스크 확장 (98G→455G), /mnt/storage 구성, 백업 자동화, SSL 복구
