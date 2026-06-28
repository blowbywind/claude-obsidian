---
date: 2026-06-20
bot: dex
type: web-research
tags: [self-learning, industry best practices, new tools and libraries, common pitfalls]
---

# 덱스 자가학습 — 2026-06-20

---

## 오늘 배운 것

- **LLM Wiki lint 오퍼레이션**: 고아 노트 탐지를 별도 수작업이 아닌 구조 검사(lint) 파이프라인으로 자동화 — 고아 페이지·깨진 크로스레퍼런스·스테일 임베딩·소스 누락을 한 번에 체크하는 패턴이 2026 기준 표준화 추세. (출처: LLM Wiki / Graphify Medium)
- **Leiden/Louvain 클러스터링**: 지식 그래프에서 관련 노트를 자동으로 "이웃(neighborhood)"으로 묶는 알고리즘 — 고아 노드와 밀집 허브를 시각적으로 즉시 파악 가능. 위키 구조 점검 도구로 활용 가능.
- **Bases 마이그레이션 타이밍**: 단순 TABLE 쿼리만 쓰는 Dataview 블록은 Bases로 전환 권장, 복잡 DQL은 유지 (기존 메모리와 일치). 마이그레이션 플레이북이 practicalpkm.com에 공개됨.
- **일관성 > 완벽한 도구 선택**: 2026 PKM 트렌드의 핵심 교훈 — 어떤 시스템이든 일관되게 충분히 오래 실행해야 복리 효과 발생. 도구 전환보다 운영 일관성이 더 중요.
- **팀 Obsidian 함정**: 중앙 콘텐츠 거버넌스 없이 팀 단위로 쓰면 지식 파편화 발생. 개인 위키에도 적용 — 네이밍 규칙·폴더 구조를 명시적 거버넌스 문서로 관리해야 장기적으로 일관성 유지.

## 출처

- [From Scattered Notes to a Living Knowledge Graph: Building LLM Wiki + Graphify](https://medium.com/@jsong_49820/from-scattered-notes-to-a-living-knowledge-graph-building-llm-wiki-graphify-01b4f031471a)
- [How to Migrate to Obsidian Bases from Dataview](https://practicalpkm.com/moving-to-obsidian-bases-from-dataview/)
- [Obsidian Bases: The Complete Guide to Database Views (2026)](https://got.md/obsidian-bases/)
- [Personal Knowledge Management (2026): The Honest Guide](https://www.atlasworkspace.ai/blog/personal-knowledge-management)
- [Mastering Personal Knowledge Management with Obsidian and AI](https://ericmjl.github.io/blog/2026/3/6/mastering-personal-knowledge-management-with-obsidian-and-ai/)

## 위키화 후보

- **LLM Wiki Lint Pattern**: 고아 노트·깨진 링크·스테일 임베딩을 한 번에 점검하는 구조 검사 파이프라인 개념 — 위키 유지관리 자동화 개념 노트로 가치 있음
- **Leiden/Louvain 클러스터링**: 지식 그래프 자동 군집화 알고리즘 — Graphify 연동 맥락에서 concepts/ 노트로 추가 적합

## 프로필 반영 후보 (저위험)

- `[2026-06-20]` 위키 구조 건강도 점검은 "lint" 개념으로 접근 — 고아 노트·깨진 크로스레퍼런스·소스 누락을 주기적으로 한 번에 검사하는 패턴 채택
- `[2026-06-20]` 도구 전환보다 운영 일관성 우선 — Dataview→Bases 마이그레이션 포함, 기존 시스템이 작동 중이면 일관된 운영을 먼저 안정화한 후 전환 검토

## 승인 필요 (고위험)

_(없음)_


## 추가 학습 (10:51 UTC)
## 오늘 배운 것

- **Obsidian Sync 공식 협업**: Shared Vault로 멀티유저 동기화 가능하나, 실시간 커서 공동편집(Google Docs 스타일)은 미지원. 모든 협업자가 Sync 구독 필요. 실시간 편집은 Peerdraft·Relay(CRDT) 등 서드파티 플러그인으로 보완 가능.
- **AI 수동성 함정(AI-driven passivity)**: AI가 요약·연결·조직화를 모두 대행하면 사용자가 인지적 이점을 잃는다. AI는 도우미지 대리자가 아님 — 큐레이션 결과를 반드시 사람이 검토해야 지식이 내면화된다.
- **캡처와 정리 동시 금지**: 수집하면서 동시에 정리하면 마찰이 커져 습관 자체가 깨진다. `capture-first, organize-later` 분리가 더 지속 가능하다.
- **PKM 노이즈 역상관**: PKM 가치는 노이즈에 반비례. 잘 정제된 50개 노트 > 미정제 5,000개 노트. 수집량이 아니라 사용 빈도로 시스템을 평가해야 한다.
- **도구 집착 함정**: 6개월 미만 주기로 도구를 교체하면 지식이 누적되지 않는다. 도구보다 운영 습관이 핵심.

## 출처

- [What's New in Obsidian? Your Guide to 2026's Top Features](https://eathealthy365.com/obsidian-2026-all-the-new-features-you-need-to-know/)
- [12 Common Personal Knowledge Management Mistakes (And How to Avoid Them)](https://www.dsebastien.net/12-common-personal-knowledge-management-mistakes-and-how-to-avoid-them/)
- [Personal Knowledge Management (2026): The Honest Guide](https://www.atlasworkspace.ai/blog/personal-knowledge-management)
- [Collaborate on a shared vault — Obsidian Help](https://help.obsidian.md/sync/collaborate)
- [Peerdraft — Real-time collaboration for Obsidian](https://www.peerdraft.app/)

## 위키화 후보

- `pkm-antipatterns.md` — PKM 6대 함정(수집 중독·과엔지니어링·도구집착·AI 수동성·동시 캡처정리·노이즈 과적재) 개념 노트. 기존 `note-lifecycle-management.md`와 보완 관계.

## 프로필 반영 후보 (저위험)

- `capture-first, organize-later` 원칙 — 노트 초안(draft)은 즉시 파일로 캡처하되, wikilink 통합·태깅은 별도 패스로 분리. 동시 처리 금지.
- AI 큐레이션 노트 `status: ai-curated` 유지 의무화 — AI가 생성한 노트는 사람 검증 전까지 신뢰도 하위 등급으로 처리하여 AI 수동성 함정 방지.

## 승인 필요 (고위험)

(없음)

## 신규 도구 후보 (에이전트/스킬)

(없음 — 기존 lint-pattern·orphan 탐지로 커버됨)


## 추가 학습 (18:17 UTC)
## 오늘 배운 것
- **Bases가 뷰 생태계로 확장**: 코어 Bases에 List/Table/Card 외에 서드파티 Kanban Bases View, Calendar Bases 플러그인 등장 — 날짜·상태 property를 가진 노트를 드래그로 재배치하면 frontmatter가 자동 갱신됨. 위키 운영 노트를 DB처럼 관리 가능.
- **공식 Dataview→Bases 변환기 존재**: 기존 Dataview 쿼리를 복붙해 inline Bases 블록으로 변환. 단 DQL/DataviewJS 복잡 쿼리는 여전히 비대응 — 내 기존 원칙(단순 TABLE만 Bases 후보, 복잡 DQL 유지)을 도구가 그대로 뒷받침함.
- **2026 공식 권고는 "지금은 Dataview 유지, 성숙도 따라 케이스별 이전"** — 운영 일관성 우선 원칙과 일치. DQL 엔진은 2022년부터 안정적.
- **PKM 신규 함정: 결정 피로(decision fatigue)** — 캡처한 항목마다 분류 결정을 요구하면 인지 자원이 고갈됨. `capture-first, organize-later` 분리 원칙의 근거가 됨.
- **택소노미는 부패한다(brittle taxonomy)** — 2024년 태그 체계가 2026년 삶에 안 맞음. 고정 태그 트리보다 wikilink 기반 그래프 연결이 시간이 지나도 견고. 고아 노트 감지 + 링크 통합 패턴의 정당성 강화.
- **"AI는 입력 품질만큼만 똑똑하다"** — clean·connected·well-structured 지식이 AI 큐레이션의 전제. `status: ai-curated` 하위등급 처리 + frontmatter summary 의무화가 곧 AI 품질 투자.

## 출처
- [Obsidian's New Bases Feature (Obsidian Observer)](https://medium.com/obsidian-observer/obsidians-new-bases-feature-is-the-biggest-update-since-properties-2aad08a102eb)
- [Plugins Supporting Bases (Kanban/Calendar)](https://www.obsidianstats.com/bases-support)
- [Dataview vs Datacore vs Obsidian Bases (Obsidian Rocks)](https://obsidian.rocks/dataview-vs-datacore-vs-obsidian-bases/)
- [How to Migrate to Obsidian Bases from Dataview](https://practicalpkm.com/moving-to-obsidian-bases-from-dataview/)
- [Personal Knowledge Management 2026: The Honest Guide](https://www.atlasworkspace.ai/blog/personal-knowledge-management)
- [Why PKM is Essential in 2026 (dsebastien)](https://www.dsebastien.net/why-is-personal-knowledge-management-pkm-useful/)

## 위키화 후보
- `decision-fatigue-pkm.md` — 캡처마다 분류 결정 강요 시 인지 자원 고갈, `capture-first` 원칙의 근거 개념
- `taxonomy-brittleness.md` — 고정 태그 트리의 시간적 부패 vs wikilink 그래프의 견고성

## 프로필 반영 후보 (저위험)
- Bases는 단순 뷰를 넘어 Kanban/Calendar 서드파티 뷰로 확장 중 — 상태·날짜 property 노트는 Bases 뷰 후보로 표시
- 고정 태그 택소노미는 시간이 지나면 부패하므로, 분류는 태그보다 wikilink 그래프 연결을 우선한다

## 승인 필요 (고위험)
- (없음)

## 신규 도구 후보 (에이전트/스킬)
- (없음 — 기존 llm-wiki-lint 패턴 + 고아 노트 감지로 충분)


## 추가 학습 (18:17 UTC)
## 오늘 배운 것

- **move-not-delete 아카이브 원칙**: 비활성 토픽 노트는 삭제하지 않고 `archive/` 폴더로 이동. 삭제는 지식 자본 손실, 이동은 작업 공간 정결 유지 양쪽을 동시에 달성. 현재 위키에 삭제 정책은 있으나 아카이브 이동 원칙이 명시되지 않음.
- **유지보수 주기 2단계**: 주별(노트 이름 정리·TODO 태그·중복 병합 경량 작업) + 분기별(태그 중복 병합·대분류 재정렬 심층 작업). 단일 주기 대신 이원화가 권장 표준.
- **AI 통합으로 지식 관리 부담 30–40% → 10% 미만**: 일반 텍스트 + 구조화된 노트 타입 + 에이전트 스킬 조합이 핵심. 도구보다 **구조 먼저** 확립해야 AI가 증폭제로 작동.
- **과잉 구조화 안티패턴**: 초기에 폴더·태그 체계를 과도하게 설계하면 노트 작성 마찰이 증가해 시스템 방치로 이어짐. "작성부터, 구조는 패턴이 보인 후"가 권장 순서.
- **태그 중복 병합 분기 규칙**: `obsidian-mcp-hybrid-retrieval`, `llm-wiki-pattern` 등 유사 태그가 복수 생성되는 경향 확인. 분기 1회 병합 루틴 필요.

## 출처

- [Mastering PKM with Obsidian and AI (Eric Ma, 2026)](https://ericmjl.github.io/blog/2026/3/6/mastering-personal-knowledge-management-with-obsidian-and-ai/)
- [A Systematic Guide to Obsidian 2026 (Enersys Insights)](https://enersys.co.th/en/insights/obsidian-systematic-pkm-guide-2026)
- [12 Common PKM Mistakes (dsebastien.net)](https://www.dsebastien.net/12-common-personal-knowledge-management-mistakes-and-how-to-avoid-them/)
- [7 PKMS Setup Mistakes (Medium, Theo James)](https://medium.com/@theo-james/setting-up-your-pkms-here-are-7-mistakes-you-dont-want-to-make-587bdfc8b79c)

## 위키화 후보

- **`archive-strategy`** — move-not-delete 원칙, 아카이브 폴더 운영 기준, 비활성 토픽 판단 조건 (기존 `note-lifecycle-management` 확장 또는 독립 노트)

## 프로필 반영 후보 (저위험)

- `[2026-06-21]` 비활성 노트는 삭제 대신 `archive/` 이동 (move-not-delete). 지식 자본 보존 + 작업 공간 정결 동시 달성.
- `[2026-06-21]` 태그 유지보수는 2단계 — 주별(이름·TODO 경량 정비) / 분기별(중복 태그 병합·대분류 재정렬).

## 승인 필요 (고위험)

_(없음)_


## 추가 학습 (18:17 UTC)
## 오늘 배운 것

1. **MOC(Maps of Content) 패턴 — 폴더 대안**: 노트는 하나의 폴더에만 존재하지만, 여러 MOC에서 동시에 wikilink로 참조 가능. 동일 노트를 중복 없이 다중 맥락에 배치하는 유일한 방법. 권장 구조: **얕은 폴더(최상위 구분) + MOC(탐색) + 태그(필터링)**.
   - 출처: [Obsidian Note Organization: Folders vs MOCs vs Tags](https://blog.shuvangkardas.com/obsidian-note-organization/)

2. **Obsidian 공식 CLI (2026-02 출시)**: `search`, 노트 생성, 일일 노트 관리, 콘텐츠 append 등 100개+ 명령을 터미널에서 직접 실행 가능. 자동화 파이프라인(dex 자가학습 등)에서 Obsidian 볼트 조작이 CLI로 가능해짐.
   - 출처: [Local LLM Knowledge Base Guide 2026](https://www.modemguides.com/blogs/ai-infrastructure/local-llm-knowledge-base-obsidian-setup-guide)

3. **Bases 카드 뷰 + 워크플로 그룹핑**: `status` 프로퍼티로 그룹/정렬하여 간단한 칸반 워크플로 구성 가능. `ai-curated` → `verified` 등 상태 전환 추적에 직접 활용 가능.
   - 출처: [Obsidian Bases update 2025](https://www.geeky-gadgets.com/obsidian-bases-update-2025/)

4. **프로퍼티 복수형 전환**: `tag` → `tags`, `alias` → `aliases`, `cssclass` → `cssclasses`. 기존 노트는 Format Converter 플러그인으로 일괄 마이그레이션 필요.
   - 출처: [Obsidian Bases launch — AlternativeTo](https://alternativeto.net/news/2025/8/obsidian-launches-new-bases-plugin-for-database-workflows-and-property-format-changes/)

5. **캡처 레이어가 최대 실패 지점**: LLM 통합 전에 캡처 파이프라인(모바일·이메일 인박스)이 불안정하면 아무리 정교한 검색도 효과 없음. "아키텍처 혼합은 통합 비용이 이득을 압도한다"는 원칙 확인.
   - 출처: [Build a Personal Knowledge Base With Local AI: 2026 Stack Guide](https://www.promptquorum.com/power-local-llm/local-llm-personal-knowledge-base-2026)

6. **플러그인 공급망 리스크**: 설치하는 모든 Obsidian 플러그인은 공격 표면 확장. 2026-03 LiteLLM 공급망 침해 사례 — 외부 의존성 최소화, 검증된 플러그인만 사용 원칙 필요.
   - 출처: [Build Your Own AI-Powered Knowledge Base](https://medium.com/@zaferdace/build-your-own-ai-powered-knowledge-base-with-llms-and-obsidian-535597958904)

---

## 출처
- [Obsidian Note Organization: Folders vs MOCs vs Tags](https://blog.shuvangkardas.com/obsidian-note-organization/)
- [Maps of Content: Effortless organization for notes](https://obsidian.rocks/maps-of-content-effortless-organization-for-notes/)
- [Obsidian Bases new features 2025 — Geeky Gadgets](https://www.geeky-gadgets.com/obsidian-bases-update-2025/)
- [Obsidian Bases launch — AlternativeTo](https://alternativeto.net/news/2025/8/obsidian-launches-new-bases-plugin-for-database-workflows-and-property-format-changes/)
- [Build a Personal Knowledge Base With Local AI: 2026 Stack Guide](https://www.promptquorum.com/power-local-llm/local-llm-personal-knowledge-base-2026)
- [Local LLM Knowledge Base Guide 2026 — ModemGuides](https://www.modemguides.com/blogs/ai-infrastructure/local-llm-knowledge-base-obsidian-setup-guide)

---

## 위키화 후보
- **`MOC (Maps of Content)`** — 단일 폴더 제약을 우회하는 wikilink 기반 다중 맥락 인덱스 패턴. 폴더·태그와 역할 분리 명확화.
- **`obsidian-cli`** — 2026-02 출시 공식 CLI; 볼트 자동화 파이프라인 진입점.

---

## 프로필 반영 후보 (저위험)
- `[2026-06-21]` MOC 우선 탐색 원칙 — 새 개념 노트 생성 시 관련 MOC 노트가 있으면 해당 MOC에 wikilink를 추가. 없으면 MOC 생성을 위키화 후보로 표시.
- `[2026-06-21]` YAML 프로퍼티 복수형 확인 의무 — 노트 작성 시 `tags`, `aliases`, `cssclasses` 복수형 키 사용. 기존 노트 발견 시 Format Converter 마이그레이션 표시.

---

## 승인 필요 (고위험)
_(없음)_

---

## 신규 도구 후보 (에이전트/스킬)
- `[skill] obsidian-cli-automation` — Obsidian 공식 CLI를 통해 노트 생성·검색·append를 터미널 파이프라인으로 자동화하는 스킬. 현재 Bash로 파일 직접 조작하는 방식을 CLI로 대체.
