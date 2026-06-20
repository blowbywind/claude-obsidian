---
title: "pdf_to_html — PDF 변환기"
id: "P-04"
status: "검증중"
phase: "Phase 10"
stack: [Python, PyInstaller, pdfminer.six, pdf2image, PyMuPDF, Jinja2]
created: 2026-06-13
updated: 2026-06-12
---

## 현재 상태

- **Phase**: Phase 10 — 검증 단계
- **진행 상황**: PDF → HTML 변환, Windows 단일 실행 파일(.exe) 배포

## 서버 / 인프라

| 항목 | 값 |
|------|-----|
| 배포 형태 | Windows 단일 .exe (PyInstaller) |
| 호출 방식 | 외부 프로그램이 프로세스로 호출 → stdout JSON |
| 플랫폼 | Windows (빌드) / Linux (개발) |

## 스택

- 언어: Python
- 번들: PyInstaller
- PDF 처리: pdf2image, pdfminer.six, PyMuPDF
- 렌더링: Jinja2 HTML 템플릿
- 시스템 의존: Poppler (Windows 바이너리 번들)

## 에이전트 허용 범위

| 에이전트 | 허용 | 금지 |
|---------|------|------|
| Claude Code | 설계·검토·문서화 | |
| Codex | `/home/bbw/projects/pdf_to_html/` 수정 | .venv 내부 직접 수정 |
| agy | 리서치만 | 코드 수정 불가 |

## Dev Gate

```bash
cd /home/bbw/projects/pdf_to_html
source .venv/bin/activate
pip install -r requirements.txt
```

## 위험 구역

- `references/`는 읽기만, 수정 금지
- stdout JSON 포맷 변경 시 호출 측 영향 확인 필수

## 자주 쓰는 명령

```bash
# 개발 실행
source .venv/bin/activate
python main.py input.pdf --output ./out/

# 빌드 (Windows에서)
pyinstaller pdf_to_html.spec
```

## 최근 작업

- Phase 10 검증 진행 중

## 다음 작업

- [ ] 최종 검증 및 배포 패키징

<!-- stale-todo-auto -->
> stale TODO: 50개 (2026-06-14 자동 수집)
