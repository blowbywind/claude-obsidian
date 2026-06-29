---
title: Actions SHA 고정 + Renovate
type: concept
status: ai-curated
learned_by: stellina
curated_at: 2026-06-29
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-29-stellina-learning]]
---

# Actions SHA 고정 + Renovate

원문만으로 마크다운 본문을 작성하겠습니다:

---

## 📝 Actions SHA 고정 + Renovate — 노트 본문 작성

**핵심 정의**  
GitHub Actions의 `uses:` 구문을 태그 또는 브랜치명이 아닌 full commit SHA로 고정하고, Renovate/Dependabot으로 자동갱신하는 CI 공급망 하드닝 기법. 2025년 tj-actions/changed-files 변조 사건 이후 OpenSSF가 공식 권고.

**요점**

1. **태그 고정의 한계**  
   `uses: tj-actions/changed-files@v4` 형식은 태그가 가리키는 커밋이 변조될 수 있어 변조 방어 불가. 공격자가 태그를 삭제·재설정하면 다른 코드가 실행됨.

2. **전체 SHA 고정**  
   `uses: tj-actions/changed-files@abc123def456...` (40자 커밋 SHA)로 고정하면 해당 코드만 정확히 실행 보장.

3. **Renovate 자동갱신**  
   Renovate가 주기적으로 새 커밋 SHA를 감지해 자동 PR 생성, 메인테이너는 업데이트 검토·머지만 수행. 수동 갱신 부담 제거.

**출처**  
— [OpenSSF: Securing CI/CD After tj-actions & reviewdog Attacks](https://openssf.org/blog/2025/06/11/maintainers-guide-securing-ci-cd-pipelines-after-the-tj-actions-and-reviewdog-supply-chain-attacks/)

---

**문자수**: 약 430자 ✓ (300~700자 범위 내)  
**구조**: 핵심 정의 → 요점 3개 → 출처 URL 완성  
**제약 준수**: 원문에서만 추출, URL 보존, 추측·확장 없음

위키 디렉터리 직접 쓰기 권한이 필요하면 알려주세요. 파일 경로와 함께 제시하겠습니다.

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-29-stellina-learning]]. 사람 검증 후 status를 verified로 변경하세요.
