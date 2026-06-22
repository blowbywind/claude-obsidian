---
title: `concepts/falco
type: concept
status: ai-curated
learned_by: stellina
curated_at: 2026-06-22
tags: [self-learning, ai-curated]
sources: [[episodic/2026-06-21-stellina-learning]]
---

# `concepts/falco

## Falco

**Falco**는 커널 시스템콜을 실시간으로 감시하는 CNCF 졸업 프로젝트로, 배포된 컨테이너의 이상 행위를 런타임에 탐지한다.

### 핵심 특징

- **eBPF 기반 감시** — 커널 모듈 불필요, 낮은 오버헤드로 권한 상승, 셸 스폰, 비인가 파일 접근, 예상 외 아웃바운드 연결, 암호화폐 채굴 등을 실시간 탐지. eBPF 드라이버 사용 시 커널 버전 호환성 문제 없음.

- **Defense-in-Depth 계층** — 이미지 정적 스캔(Trivy) → 입장 제어(Admission Controller) → **Falco 런타임 감시**의 3단계 방어. 배포 전 취약점 검사와 달리 배포 후 실제 실행 환경의 이상 행위를 탐지해 보안 사각 제거.

- **통합 알림** — Falcosidekick을 통해 탐지 이벤트를 Slack, PagerDuty 등으로 자동 라우팅. 심각도별 분류 및 실시간 응답 가능.

### 출처

- https://www.decryptiondigest.com/blog/container-runtime-security-falco
- https://oneuptime.com/blog/post/2026-01-28-falco-container-security/view

> 자가학습 원문에서 AI가 큐레이션한 노트. 출처: [[episodic/2026-06-21-stellina-learning]]. 사람 검증 후 status를 verified로 변경하세요.
