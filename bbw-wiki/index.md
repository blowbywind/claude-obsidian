# BBW Wiki Index

> 에이전트가 유지하는 전체 위키 카탈로그. 질의 시 이 파일을 **먼저, 그리고 유일하게** 읽는다.
> 필요한 페이지만 선택 로드 (최대 3개). raw/ 재읽기 금지. queries/ 캐시 우선 확인.

---

## Sources

- [SeaweedFS — 분산 오브젝트 스토리지 종합 문서](wiki/sources/2026-06-12-seaweedfs-docs.md) — v4.23 BBW 운용 현황, Needle·Volume·Filer·S3 아키텍처, Erasure Coding, MinIO 비교, AWS SDK 연동, Docker 배포
- [LLM Wiki가 망하는 진짜 이유 — Brain Trinity AI OS 설계](wiki/sources/2026-05-16-llm-wiki-failure-brain-trinity.md) — LLM Wiki 실패 3원인(목적 부재·완벽주의·방법론만 복제), LLM Wiki=얕은 컴파일, 철학→역할→행동→지식 계층, GOLD IN GOLD OUT
- [Hermes Agent v0.16.0 — 실제 설치·명령 체계·BBW 운용 현황](wiki/sources/2026-06-12-hermes-agents.md) — hermes --help/status/config 직접 조사: gateway·cron·skills·MCP·ACP·worktree·oneshot 전체 명령 체계, BBW P0 미완료 목록
- [hermes dashboard 외부 접속 — KT hairpin NAT 성공 사례](wiki/sources/2026-06-12-hermes-external-access.md) — KT GiGA WiFi Home hairpin NAT으로 snowball.me.kr:9119 접속 성공, 실패 시도 목록, Caddy trusted_proxies 설정
- [Caddy v2 공식 문서 — 리버스 프록시·자동 HTTPS·Caddyfile 종합](wiki/sources/2026-06-12-caddy-v2-docs.md) — 자동 HTTPS 원리, Caddyfile 문법, Docker 배포, inode 바인드 마운트 함정, HTTP/3 설정
- [[60회 AI&UX세미나] AI 네이티브 UX/UI 디자인 시대](wiki/sources/2026-05-28-ai-native-ux-lm-wiki-60th-seminar.md) — 유훈식 교수의 6단계 워크플로우, AI 임베디드 vs AI 네이티브, 합성 사용자, 마크다운 85% 토큰 절감+35% 속도향상
- [자유령 에이전트 3종 비교 — 헤르메스·OpenClaw·Gemini Spark](wiki/sources/2026-06-10-free-roaming-agents-comparison.md) — 로컬(헤르메스·OpenClaw) vs 클라우드(Gemini Spark) 비교, LM 위키×옵시디언 실무 UX 워크플로우, 마크다운 토큰 65-90% 절감
- [프롬프트의 시대는 끝났다 — 루프를 설계하라](wiki/sources/2026-06-10-loop-design-kimyoil.md) — 김요일이 해설하는 Boris Cherny 루프 철학: 프롬프트→loop.md 진화, 3가지 검증 기준, PR 모니터링 루프
- [AI 네이티브 운영 방법 — 헤르메스 에이전트 실무 적용기](wiki/sources/2026-06-09-ai-native-hermes-report.md) — 김요일의 헤르메스 5명+Claude Code 5명 AI 네이티브 팀, 야간 자율 학습 루프, 옵시디언 위키 맥락 공유 실전기
- [옵시디언 아직도 그냥 쓰세요? 클로드 스타일로 바뀝니다!](wiki/sources/2026-06-08-obsidian-claude-style-css-mr5pm.md) — CSS 스니펫+Claude Code로 Obsidian을 Claude 인터페이스 스타일(다크·주황·명조)로 실시간 커스터마이징하는 워크플로우
- [클로드코드 직접 만든 사람이 직접 공개한 사용법 - '하네스'](wiki/sources/2026-06-08-claude-code-harness-castlestudio.md) — Anthropic 실험: 동일 모델 $9(고장) vs $200(완동)의 유일한 차이는 Planner-Generator-Evaluator 구조
- [AI를 기존 방식에 얹지 마세요 — 워크플로우를 통째로 갈아엎어야 하는 이유](wiki/sources/2026-06-08-ai-workflow-overhaul-silval-dev.md) — 하재상·알렉스(Meta 엔지니어)의 AI 시대 위임 마인드셋·에이전트 프로덕티비티·컨텍스트 인텔리전스 실전 강연
- [에이나우 클로드코드 실전 마스터가이드 v1.0](wiki/sources/2026-06-07-ainow-claude-code-master-guide.md) — Boris Cherny 42가지 팁·해커톤 노하우·업종별 실전 프로젝트를 담은 한국어 Claude Code 실전 가이드북
- [하네스 엔지니어링 기초 가이드북](wiki/sources/2026-06-07-harness-engineering-guide.md) — Hashimoto 정의부터 OpenAI·Anthropic·Stripe 실전 사례까지, 프롬프트→컨텍스트→하네스 3단계 진화 체계
- [LLM Wiki를 업그레이드하는 외부 지식 시스템: Zotero × NotebookLM × Obsidian × Claude Code](wiki/sources/2026-06-07-zotero-notebooklm-llm-wiki-upgrade.md) — Zotero(원본 도서관)+NotebookLM(심층 Q&A)으로 LLM Wiki를 완성하는 3계층 외부 지식 아키텍처
- [How I Use Obsidian + Claude Cowork to Run My Life](wiki/sources/2026-06-07-obsidian-claude-cowork-ai-os-nick-milo.md) — Nick Milo의 AI OS 3레이어 아키텍처: Ideaverse·번역층·Cowork 통합 실전 가이드
- [LLM Wiki — 개인 지식 베이스 구축 패턴](wiki/sources/2026-06-05-llm-wiki-pattern.md) — LLM이 유지하는 영구적 위키로 RAG를 대체하는 지식 축적 패턴
- [How Claude Code Works](wiki/sources/2026-06-05-how-claude-code-works.md) — Claude Code 공식 문서: 에이전트 루프·도구·컨텍스트·세션 관리 아키텍처
- [왕초보를 위한 클로드코드 설치 30분 강의](wiki/sources/2026-06-05-claude-code-beginner-install-guide.md) — 한국어 유튜브 강의, 설치부터 CLAUDE.md·에이전트 워크플로우 기초까지
- [클로드 코드를 정말 잘 쓰는 7단계 테크트](wiki/sources/2026-06-05-claude-code-7steps-mastery.md) — 설치→CLAUDE.md→커맨드→스킬→에이전트→MCP→훅스 7단계 프레임워크
- [Claude Code + Obsidian + LM Wiki + Graphify 실습 가이드](wiki/sources/2026-06-05-claude-code-obsidian-lmwiki-graphify.md) — 브레인 트리니티의 LM Wiki + Graphify 전 과정 실습 (볼트 생성 → 스킬 → 그래프 DB)
- [hnedu-auth 프로젝트 지침 (CLAUDE.md)](wiki/sources/2026-06-05-hnedu-auth-project.md) — 해냄에듀 통합 인증 서비스 구조·배포·보안·반복 작업 기록

---

## Concepts

- [합성 사용자](wiki/concepts/synthetic-user.md) — 실제 UX 데이터 기반 LLM 모델링 가상 사용자: 실시간 대화, 데이터 누적 후 조사 대체 가능
- [자유령 에이전트](wiki/concepts/free-roaming-agent.md) — 개인 소유 자율 AI 에이전트 카테고리: 헤르메스·OpenClaw·Gemini Spark 3종 비교, 로컬 vs 클라우드, 선택 기준
- [루프.md 패턴](wiki/concepts/loop-md.md) — AI 완료 선언 전 자기 검증 강제하는 메타 레이어: 필수 통과·측정·평가 3기준 + PR 모니터링 루프
- [AI 네이티브 팀 구성](wiki/concepts/ai-native-team.md) — 헤르메스(에이전시)·Claude Code(인하우스) 역할 분리 기반 10명 AI 팀 운영 구조
- [야간 자율 학습 루프](wiki/concepts/autonomous-learning-loop.md) — 크론잡으로 에이전트가 취침 중 자율 학습, 결과를 옵시디언 위키화해 메모리 효율 유지
- [AI 오케스트레이터 마인드셋](wiki/concepts/ai-orchestrator-mindset.md) — 직접 실행하는 사람에서 에이전트에게 위임·조율하는 사람으로의 전환, 워크플로우 재정의 4단계
- [컨텍스트 인텔리전스](wiki/concepts/context-intelligence.md) — 세컨 브레인에 구조·인덱스를 부여해 에이전트가 필요할 때 필요한 정보만 가져오게 하는 전략 (Meta 사례: 2h→30min)
- [하네스 엔지니어링](wiki/concepts/harness-engineering.md) — AI 에이전트를 제약·툴·피드백·관찰로 제어하는 2026년 신 패러다임 (Hashimoto 정의)
- [컨텍스트 엔지니어링](wiki/concepts/context-engineering.md) — 모델에게 적절한 정보를 적절한 시점에 제공하는 문맥 설계 기술 (Karpathy 2025)
- [Generator-Evaluator 패턴](wiki/concepts/generator-evaluator-pattern.md) — 생성과 평가를 분리하는 Anthropic 멀티 에이전트 설계 패턴
- [Boris 자기학습 루프](wiki/concepts/boris-self-learning-loop.md) — 에이전트 실수마다 CLAUDE.md에 방지 규칙을 추가해 시스템을 점진적으로 성장시키는 방법론
- [외부 지식 시스템](wiki/concepts/external-knowledge-system.md) — Zotero·LLM Wiki·NotebookLM 3계층 외부 지식 아키텍처, Claude Code MCP로 통합
- [Brain Trinity](wiki/concepts/brain-trinity.md) — 삶의 철학→역할→목표→행동→지식 계층 기반 AI OS 설계 프레임워크, LLM Wiki=얕은 컴파일, My Notes=깊은 이해, GOLD IN GOLD OUT
- [AI OS (AI 운영체제)](wiki/concepts/ai-os.md) — Ideaverse·번역층·외부 AI 3레이어로 구성된 이식 가능한 개인 AI 시스템 (Brain Trinity 관점 추가)
- [ME.MD (AI 포터블 아이덴티티)](wiki/concepts/me-md.md) — AI-agnostic 포터블 아이덴티티 파일, CLAUDE.md의 범용 버전
- [ACE 폴더 프레임워크](wiki/concepts/ace-folder-framework.md) — Nick Milo의 Atlas·Calendar·Efforts Obsidian 볼트 구조
- [Vault Map & Skill Map](wiki/concepts/vault-map.md) — AI가 볼트를 탐색하고 스킬을 선택하도록 안내하는 번역층 핵심 파일
- [LLM Wiki 패턴](wiki/concepts/llm-wiki-pattern.md) — LLM이 점진적으로 유지하는 마크다운 위키 기반 지식 관리 시스템
- [RAG (Retrieval-Augmented Generation)](wiki/concepts/rag.md) — 질의 시마다 문서에서 청크를 검색해 답변을 생성하는 방식
- [Memex](wiki/concepts/memex.md) — Vannevar Bush(1945)가 제안한 개인 지식 저장·연결 시스템 개념
- [세컨드 브레인](wiki/concepts/second-brain.md) — 외부 시스템에 지식을 체계적으로 축적·연결하는 개인 지식 관리 방식
- [에이전트 루프](wiki/concepts/agentic-loop.md) — LLM 에이전트의 맥락파악→조치→검증 반복 실행 패턴
- [컨텍스트 윈도우](wiki/concepts/context-window.md) — LLM이 한 번에 처리하는 정보 공간, 관리 전략
- [CLAUDE.md](wiki/concepts/claude-md.md) — Claude Code 세션 간 영속하는 프로젝트별 지시 파일
- [AI 에이전트 워크플로우](wiki/concepts/ai-agent-workflow.md) — 검증 가능한 데이터·명확한 지시로 AI 반복 작업을 자동화하는 패턴
- [MCP (Model Context Protocol)](wiki/concepts/mcp.md) — AI와 외부 도구(노션·구글·GitHub 등)를 연결하는 다리
- [훅스 (Hooks)](wiki/concepts/hooks.md) — Claude Code 자동화 트리거 (preToolUse/postToolUse/notification)
- [커맨드 & 스킬스](wiki/concepts/claude-code-commands-skills.md) — 반복 업무 단축 명령(커맨드) vs 순서 실행 워크플로우(스킬스)
- [Graphify](wiki/concepts/graphify.md) — Obsidian 마크다운을 지식 그래프(JSON)로 변환해 LLM이 그래프 탐색 쿼리를 수행하는 도구
- [목적성 있는 수집](wiki/concepts/purposeful-collection.md) — "왜 수집했는지 설명 가능한" 의도적 큐레이션, Gold in Gold out 원칙
- [JWT RS256 인증 패턴](wiki/concepts/jwt-rs256.md) — 비대칭키 JWT 서명, 인증 서버만 개인키 보유하고 각 서비스는 공개키 검증만 수행
- [hnedu-auth 배포 워크플로우](wiki/concepts/hnedu-auth-deploy.md) — build → scp → docker logs 3단계 수동 프로세스 및 자동화 후보 정리
- [Caddy](wiki/concepts/caddy.md) — 자동 HTTPS·Caddyfile·reverse_proxy·log 디렉티브, Docker inode 함정, caddy reload vs restart, HTTP/3 설정법
- [KT hairpin NAT](wiki/concepts/kt-hairpin-nat.md) — KT GiGA WiFi Home의 NAT loopback 동작, remote_ip:172.30.1.254 진단법, 서버 자체 테스트 실패 이유
- [Hermes 아키텍처](wiki/concepts/hermes-architecture.md) — gateway·스킬·크론·MCP/ACP·프로필·컨텍스트 압축 6개 레이어, oneshot/worktree/send 패턴
- [SeaweedFS 아키텍처](wiki/concepts/seaweedfs-architecture.md) — Needle(45B 오버헤드)·Volume(.dat/.idx)·Filer 메타데이터·S3 게이트웨이 3계층, Erasure Coding RS(10,4), weed server/mini/cluster 모드

---

## Entities

- [SeaweedFS](wiki/entities/seaweedfs.md) — Apache-2.0 분산 오브젝트 스토리지, v4.23 BBW 운용 중 (storage_seaweedfs), S3 API·FUSE·WebDAV 지원, MinIO 대안
- [Caddy (Web Server)](wiki/entities/caddy.md) — Go 기반 오픈소스 웹서버·리버스프록시, 자동 HTTPS, v2.11.4, GitHub 73.3k stars, bbw 홈서버 운용 중
- [유훈식 교수](wiki/entities/yu-hunsik.md) — 서울 미디어 대학원대학교, AI4UX 채널 운영, AI 네이티브 UX 6단계 워크플로우·합성 사용자 제안
- [Gemini Spark](wiki/entities/gemini-spark.md) — Google IO 2026 발표 클라우드 개인 AI 에이전트, Google 생태계 통합, 한국 1-4개월 출시 예상
- [김요일](wiki/entities/kimyoil.md) — 1인 기업 대표, 헤르메스+Claude Code AI 네이티브 팀 운영 실전기 공유
- [헤르메스 에이전트](wiki/entities/hermes-agent.md) — v0.16.0 설치 완료, gpt-5.5/Codex OAuth, docker 터미널, dashboard :9119 외부 접속 가능, gateway·cron·skills·MCP 지원
- [OpenClaw](wiki/entities/openclaw.md) — 로컬 셀프호스팅 AI 에이전트 (2026.01, Telegram·Slack 등 22채널, 헤르메스 유사)
- [OpenDesign](wiki/entities/opendesign.md) — Claude Design 로컬화 오픈소스, 무한 루프 UI 실습 도구
- [오후다섯씨 (Mr.5pm)](wiki/entities/mr5pm.md) — AI 활용·생산성 유튜브 채널, Claude 스타일 Obsidian CSS 스니펫 제작·배포
- [castlestudio](wiki/entities/castlestudio.md) — AI 활용법 한국어 유튜브 채널, Anthropic 하네스 실험 결과 해설
- [하재상 (실밸개발자)](wiki/entities/silval-dev-jaesung.md) — Meta 8년차 엔지니어·실밸개발자 유튜버, AI 오케스트레이터 마인드셋·컨텍스트 인텔리전스 제안자
- [알렉스 (커리어에커 알렉스)](wiki/entities/career-echo-alex.md) — Meta 8년차 엔지니어·커리어에커 유튜버(~20만), AI 네이티브·24시간 에이전트 전문
- [에이나우](wiki/entities/ainow.md) — 신영선이 운영하는 1만 명 한국어 AI 커뮤니티, Claude Code·하네스 엔지니어링 실전 가이드 출판
- [Boris Cherny](wiki/entities/boris-cherny.md) — Anthropic Staff Engineer, Claude Code 창시자, 42가지 팁·자기학습 루프 방법론
- [Mitchell Hashimoto](wiki/entities/mitchell-hashimoto.md) — HashiCorp 공동창업자·Terraform 창시자, 하네스 엔지니어링 개념 최초 정의 (2026.02.05)
- [Zotero](wiki/entities/zotero.md) — 원본 소스 레퍼런스 매니저, Zotero MCP로 Claude Code 연동
- [NotebookLM](wiki/entities/notebooklm.md) — Google AI 연구 도구, 고정 소스 기반 Q&A·아웃풋 생성, notebooklm.py MCP 연동
- [Nick Milo](wiki/entities/nick-milo.md) — Ideaverse·ACE·AI OS 프레임워크 창시자, Obsidian PKM 전문가
- [Vannevar Bush](wiki/entities/vannevar-bush.md) — Memex 개념을 제안한 과학자·행정가 (1945)
- [Obsidian](wiki/entities/obsidian.md) — 마크다운 기반 로컬 노트 앱, 그래프 뷰·플러그인 생태계 보유
- [qmd](wiki/entities/qmd.md) — 마크다운 파일용 로컬 하이브리드 검색 엔진 (BM25/벡터, MCP 지원)
- [Claude Code](wiki/entities/claude-code.md) — Anthropic의 터미널 기반 에이전트형 코딩 도우미, bbw-wiki 유지 도구
- [Anthropic](wiki/entities/anthropic.md) — Claude·Claude Code 개발사
- [Antigravity](wiki/entities/antigravity.md) — Google이 만든 AI 통합 개발 환경, Gemini 연동
- [Cowork](wiki/entities/cowork.md) — Claude 앱과 함께 사용하는 AI 도구, Claude Code로 대체 가능
- [Graphify (도구)](wiki/entities/graphify.md) — 지식 그래프 생성 Python 라이브러리, Karpathy LM Wiki 트윗 후 48시간 만에 제작
- [브레인 트리니티](wiki/entities/brain-trinity.md) — 한국어 PKM + AI 유튜브 채널, bbw-wiki의 주요 소스
- [hnedu-auth](wiki/entities/hnedu-auth.md) — 해냄에듀 사내 통합 인증 서비스, JWT RS256 발급·직원·부서·역할 관리
- [hnedu-erp](wiki/entities/hnedu-erp.md) — 해냄에듀 ERP (WinForms C# + .NET Web API), hnedu-auth JWT 검증 연동
- [hnedu-crm](wiki/entities/hnedu-crm.md) — 해냄에듀 CRM (Next.js 15 + FastAPI), hnedu-auth JWT 검증 연동

---

## Queries

- [Claude Code ↔ Wiki 관계 전략](wiki/queries/2026-06-06-claude-wiki-relationship.md) — 코인 절약·반복질문 제거·정보유실 방지를 위한 운영 전략 [workflow][cost]
