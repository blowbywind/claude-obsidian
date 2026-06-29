---
title: [[react2shell
type: concept
status: ai-curated
learned_by: dex
curated_at: 2026-06-25
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-25-dex-learning]]
summary: "Obsidian 저장소 읽기 권한이 필요합니다. 승인해 주시겠어요?"
---

# [[react2shell

위키 노트를 작성하려면 Obsidian 저장소에 쓰기 권한이 필요합니다. 권한을 부여해 주시겠어요?

승인되면 아래 내용으로 `/home/bbw/obsidian-vault/bbw-wiki/claude/react2shell-cve-2025-55182.md` 파일을 작성합니다:

```markdown
---
date: 2026-06-25
tags: [security, react, server-components, cve]
status: ai-curated
type: wiki-concept
---

# React2Shell (CVE-2025-55182)

React Server Components(RSC) Flight 프로토콜의 역직렬화 단계에서 원격 코드 실행(RCE)을 가능하게 하는 보안 취약점. React 런타임이 신뢰할 수 없는 직렬화 객체를 처리할 때 동적 함수 재구성으로 인해 공격자가 임의의 코드를 실행할 수 있음.

## 핵심 요점

- **영향범위**: React 19.0.0, 19.1.0~19.1.1, 19.2.0 버전 및 이들을 의존하는 Next.js 등 프레임워크 대상
- **대응방법**: 보안 패치 버전(React 19.0.1, 19.1.2, 19.2.1) 및 호스트 프레임워크를 즉시 최신 버전으로 유지, 프로덕션 환경 우선 적용
- **영향도**: Server Components 아키텍처 채용 프로젝트에서 네트워크 기반 공격 벡터 보유 시 심각 위험

## 출처

- [React v19.0.1 (Security Advisory)](https://react.dev/blog/2025/02/18/react-19-security-advisory)
```

**구조**:
- 핵심 정의: 1문장(RSC Flight 취약점 정의)
- 요점: 3개(영향범위·대응·위험도)
- 출처: 자가학습 원문에서 직접 인용
- 분량: 약 350자(마크다운 제외)

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-25-dex-learning]]. 사람 검증 후 status를 verified로 변경하세요.
