---
title: hnedu-auth 배포 워크플로우
type: concept
tags: [deploy, hnedu, workflow, automation]
created: 2026-06-05
updated: 2026-06-05
sources: [2026-06-05-hnedu-auth-project]
---

## 정의

hnedu-auth 관리자 UI 변경 사항을 프로덕션 서버에 반영하는 수동 3단계 프로세스. 현재 스크립트화되지 않아 매번 명령어를 직접 입력해야 한다.

## 현재 배포 절차 (수동 3단계)

```bash
# Step 1 — 빌드 (로컬)
cd /home/bbw/projects/hnedu_auth/admin-ui
pnpm build

# Step 2 — 서버 업로드
scp -r ../public/admin hnedu-server:/var/web-infra/hnedu_auth/public/

# Step 3 — 상태 확인
ssh hnedu-server "docker logs hnedu_auth --tail 10"
```

## 서버 직접 작업 시 PATH 문제

SSH 비대화형 세션에서는 `~/.profile`이 로드되지 않아 pnpm PATH 누락:

```bash
# 모든 서버 pnpm 명령 앞에 PATH 명시 필수
PATH=~/.local/bin:~/.npm-global/bin:$PATH pnpm <command>

# 또는 prisma 직접 실행
node_modules/.bin/prisma migrate dev --name <이름>
```

## Prisma 스키마 변경 루틴 (2단계)

```bash
pnpm db:migrate    # 마이그레이션 적용
pnpm db:generate   # 클라이언트 재생성
# (필요 시) pnpm db:seed
```

## DB 시드 주의사항

`upsert`에 `update: {}` 사용 시 기존 데이터 미갱신. 역할 데이터 변경 시:

```ts
// 반드시 update 필드에 description 포함
await prisma.systemRole.upsert({
  where: { systemCode_roleCode: { ... } },
  update: { description: r.description },  // ← 필수
  create: r,
})
```

역할 코드 삭제/변경이 필요한 경우 수동 SQL 직접 실행:

```sql
DELETE FROM system_roles WHERE system_code = 'CRM' AND role_code = 'OLD_ROLE';
```

## 자동화 후보

| 작업 | 현재 방식 | 스크립트화 방안 |
|------|----------|----------------|
| UI 배포 | build → scp → 확인 (3단계 수동) | `deploy-admin.sh` 또는 Claude Code 스킬 |
| 서버 PATH | 매번 명시 | `.bashrc` or ssh alias 설정 |
| Prisma 변경 | 2단계 수동 | `pnpm db:migrate && pnpm db:generate` 하나로 묶기 |
| 배포 후 확인 | docker logs 수동 | 배포 스크립트에 포함 |

## 관련 개념

- [[wiki/concepts/ai-agent-workflow|AI 에이전트 워크플로우]] — 자동화 패턴 참조

## 관련 엔티티

- [[wiki/entities/hnedu-auth|hnedu-auth]]

## 출처

- [[wiki/sources/2026-06-05-hnedu-auth-project]]
