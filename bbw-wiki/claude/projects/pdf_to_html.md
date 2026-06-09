# pdf_to_html

## 핵심
PDF → HTML 변환기. Windows 단일 실행 파일(.exe)로 배포. 외부 프로그램이 프로세스로 호출.

## 현재 상태
- 위치: `/home/bbw/projects/pdf_to_html`
- 기획서: `기획서.md`
- Python 가상환경: `.venv/`

## 개발 환경
- Linux 개발: `source .venv/bin/activate`
- Windows 빌드: `.venv\Scripts\activate`
- 의존성: `pip install -r requirements.txt`
- Poppler: `poppler/bin/` (Windows용, PyInstaller 번들)

## 아키텍처
- `main.py` — CLI 진입점 (argparse, exit code, stdout JSON)
- 외부 호출 → stdout JSON 결과 반환

## 작업 히스토리
- (기록 없음)
