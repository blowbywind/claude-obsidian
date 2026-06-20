---
title: "hnedu_auth 배포 런북"
type: runbook
tags: [hnedu_auth, deployment, runbook]
created: 2026-06-13
updated: 2026-06-13
---

# hnedu_auth 배포 런북

> PM-2 산출물 | 실측 기준: 2026-06-13

## 서버 정보

| 항목 | 값 |
|------|-----|
| SSH 별칭 | `hnedu-server` |
| 서버 IP | 192.168.0.221 (LAN) |
| 서버 경로 | `/var/web-infra/hnedu_auth/` |
| 외부 도메인 | `auth.snowball.me.kr` |
| 헬스체크 (LAN) | `http://192.168.0.221:3100/health` |
| 헬스체크 (외부) | `https://auth.snowball.me.kr/health` |
| 프로세스 | Docker Compose (`hnedu_auth` 컨테이너) |
| DB | PostgreSQL (TimescaleDB PG17, `db_postgres`) |
| 현재 Phase | Phase 11 완료 ✅ — 실서비스 연동 대기 |

---

## 배포 절차

### 일반 배포 (코드 변경)

```bash
# 로컬에서 서버로 변경 사항 전송
ssh hnedu-server "cd /var/web-infra/hnedu_auth && git pull"

# 또는 Docker 이미지 재빌드
ssh hnedu-server "cd /var/web-infra && docker compose up -d --build hnedu-auth"
```

### Admin UI 배포 (Next.js 빌드)

```bash
# 로컬: 빌드
cd /home/bbw/projects/hnedu_auth/admin-ui
pnpm build

# 서버로 전송 (public/admin/ 직접 수정 금지 — 빌드 결과물만 전송)
scp -r ../public/admin hnedu-server:/var/web-infra/hnedu_auth/public/

# ⚠️ public/admin/ 파일을 직접 편집하지 않는다 — 빌드 시 전체 교체됨
```

### DB 마이그레이션

```bash
ssh hnedu-server "cd /var/web-infra/hnedu_auth && \
  PATH=~/.local/bin:~/.npm-global/bin:\$PATH \
  node_modules/.bin/prisma migrate deploy"
```

---

## 재시작

```bash
# 컨테이너 재시작
ssh hnedu-server "cd /var/web-infra && docker compose restart hnedu-auth"

# 전체 스택 재시작 (DB 포함)
ssh hnedu-server "cd /var/web-infra && docker compose down && docker compose up -d"

# 로그 확인
ssh hnedu-server "docker logs hnedu_auth --tail=50 -f"
```

---

## 롤백

```bash
# 이전 컨테이너 이미지로 롤백
ssh hnedu-server "cd /var/web-infra && \
  docker compose pull hnedu-auth && \
  docker compose up -d hnedu-auth"

# 또는 git revert 후 재배포
ssh hnedu-server "cd /var/web-infra/hnedu_auth && \
  git revert HEAD && \
  cd /var/web-infra && docker compose up -d --build hnedu-auth"
```

---

## JWT 키 로테이션

> **⚠️ 영향**: hnedu_crm, hnedu_erp 모두 공개키 업데이트 필요

```bash
# 새 키 생성 (서버에서)
ssh hnedu-server "cd /var/web-infra/hnedu_auth && \
  openssl genrsa -out keys/private.pem.new 2048 && \
  openssl rsa -in keys/private.pem.new -pubout -out keys/public.pem.new"

# 검증 후 교체
ssh hnedu-server "cd /var/web-infra/hnedu_auth/keys && \
  mv private.pem private.pem.bak && mv private.pem.new private.pem && \
  mv public.pem public.pem.bak && mv public.pem.new public.pem"

# 재시작
ssh hnedu-server "cd /var/web-infra && docker compose restart hnedu-auth"

# ⚠️ 이후 hnedu_crm, hnedu_erp에 새 공개키 배포 필수
```

---

## UFW 설정 (sudo 필요)

```bash
ssh hnedu-server
sudo ufw status numbered

# auth 포트 (3100) — Docker 내부, 외부 직접 노출 없음
# Caddy가 443으로 프록시

# Docker↔UFW 충돌 방지 (이미 적용됨 — 확인용)
cat /etc/docker/daemon.json
```

---

## 헬스체크 확인

```bash
# 외부
curl https://auth.snowball.me.kr/health

# LAN
curl http://192.168.0.221:3100/health

# 공개키 확인
curl https://auth.snowball.me.kr/auth/public-key
```

---

## 장애 대응

| 증상 | 원인 | 조치 |
|------|------|------|
| 컨테이너 재시작 후 인터넷 끊김 | Docker↔UFW iptables 충돌 | `/etc/docker/daemon.json` + UFW after.rules 확인 |
| 401 Unauthorized (JWT 검증 실패) | 공개키 미동기화 | hnedu_crm·hnedu_erp에 공개키 재배포 |
| pnpm install 중 인터넷 불안정 | 가정용 업로드 대역폭 포화 | 서버에서 직접 실행 |
| DB 마이그레이션 drift | schema.prisma 불일치 | `prisma migrate status` 확인 후 resolve |

---

## 의존 관계

| 서비스 | 의존 방향 | 주의사항 |
|--------|---------|---------|
| hnedu_crm | → hnedu_auth 공개키 검증 | JWT 키 로테이션 시 동기화 필수 |
| hnedu_erp | → hnedu_auth 공개키 검증 | JWT 키 로테이션 시 동기화 필수 |

> 상세 의존 관계 정책: `40-decisions/policies/auth-change-policy.md`
