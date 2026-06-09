# claude-config (.claude 설정)

## 핵심
Claude Code 글로벌 설정. 위치: `~/.claude/`
모든 프로젝트에 공통 적용되는 규칙·훅·메모리·스킬 관리.

## 현재 구조
```
~/.claude/
  CLAUDE.md              ← 핵심 원칙, 말투, 에이전트 아키텍처
  settings.json          ← 권한, 훅 등록
  memory/
    active-rules.md      ← 세션 시작 시 자동 주입되는 영구 규칙
    lessons.md           ← 실수 기록 로그
    stack-notes.md       ← 기술 스택 (Next.js 15, Fastify, PostgreSQL 등)
    server-network-warning.md ← 서버 작업 주의사항
  hooks/
    session-start/load-context.sh  ← 세션 시작 시 컨텍스트 주입 (Obsidian 노트 포함)
    pre-tool-use/block-dangerous.sh
    pre-tool-use/block-env-read.sh
    post-tool-use/auto-format.sh
```

## 메모리 시스템
- `memory/` — Claude 전용 규칙·스택 메모리
- `obsidian-vault/bbw-wiki/claude/projects/` — 프로젝트별 맥락 (양방향)
- 세션 시작 시 `load-context.sh`가 현재 프로젝트 노트를 자동 주입

## active-rules 현황 (2026-06-08)
1. bash 배열 글로브 패턴 주의
2. hook 테스트는 `bash -n` 사용
3. 조건부 실행 지시("확인 후", "승인하면" 등) → 즉시 실행 금지
4. 위험 명령어(`rm -rf` 등) 제안 전 현재 상태 먼저 확인

## 주요 결정 이유
- **Python으로 JSON 직렬화**: 서버에 jq 미설치 → `python3 -c json.dumps` 사용
- **Obsidian 연동**: 대화 종료 시 메모리 초기화 문제 해결. 프로젝트 노트를 세션 시작 시 주입.
- **active-rules 분리**: lessons.md는 기록용, active-rules.md는 실제 동작 규칙 — 역할 분리

## 작업 히스토리
- 2026-06-08: Obsidian 프로젝트 노트 연동, load-context.sh 업데이트
- 2026-06-07: 조건부 실행 금지 규칙 추가 (배지 통합 사고)
- 2026-06-04: 잘못된 파일 수정 방지 규칙 추가
