---
name: rollback-prevention
description: ai-ops 변경물이 원인 모르게 되돌아가지 않도록 막는 자동 저장과 파괴적 git 차단 원칙.
metadata:
  type: feedback
summary: "성공한 변경을 빨리 커밋하고 파괴적 git 명령을 차단하여 미커밋 상태의 작업 유실을 방지하는 체계"
---

# rollback-prevention

성공한 변경이 미커밋 상태로 오래 남으면 `reset`, `restore`, `checkout`, `clean`, `stash` 같은 동작이나 자동화 충돌로 유실될 수 있습니다.

## 원칙
- 성공 변경은 가능한 빨리 git 이력에 남긴다.
- 파괴적 git 명령은 기본 차단한다.
- 작업 로그는 위키와 로컬 작업 기록에 함께 남긴다.

## 관련
- [[effective-improvement-workflow]]
- [[autobots-identity]]
