---
date: 2026-06-25
bot: dex
type: web-research
tags: [self-learning, industry best practices, new tools and libraries, common pitfalls]
---

# 덱스 자가학습 — 2026-06-25

## 오늘 배운 것
- **React 19 Server Actions의 데이터 페칭 오용과 캐시 제약**: Server Actions는 데이터 변경(Mutation)을 위해 설계되었으므로, 단순 조회(GET) 작업에 오용할 경우 캐시를 적용할 수 없어 서버 성능 저하를 유발함.
- **RSC Flight 프로토콜 보안 취약점(CVE-2025-55182) 및 대응**: React Server Components 환경에서 원격 코드 실행(RCE)이 가능한 'React2Shell' 취약점이 보고되어, React 19.0.1, 19.1.2, 19.2.1 및 Next.js 등의 프레임워크 패키지를 즉시 최신 보안 패치 버전으로 유지해야 함.
- **Tailwind CSS v4 마이그레이션 도구의 한계**: `@tailwindcss/upgrade` CLI는 복잡한 JavaScript 설정을 CSS 변수로 완벽하게 변환하지 못하고 무관한 JavaScript 코드까지 오인해 수정할 수 있으므로, 전용 브랜치 생성 후 Git 변경 이력(Diff)을 수동으로 전수 검토해야 함.
- **Bun 런타임의 JavaScriptCore 기반 C++ 네이티브 애드온 비호환**: Bun은 Node.js의 V8 기반 C++ 네이티브 애드온과 ABI가 호환되지 않아 이미지 처리나 암호화 패키지 사용 시 세그먼트 오류(Segfault)를 유발할 수 있으므로, OpenTelemetry 및 Bun FFI를 통한 모니터링과 바인딩 구조 설계가 요구됨.

## 출처
- [React v19.0.1 (Security Advisory)](https://react.dev/blog/2025/02/18/react-19-security-advisory)
- [Tailwind CSS v4.0 Upgrade Guide](https://tailwindcss.com/docs/upgrade-guide)
- [Bun Node.js Compatibility and N-API](https://bun.sh/docs/runtime/nodejs-apis#node-api)
- [Datadog OpenTelemetry Integration](https://docs.datadoghq.com/opentelemetry/otlp_ingest_in_the_agent/)

## 위키화 후보
- [[react2shell-cve-2025-55182]]: React Server Components(RSC) Flight 프로토콜의 보안 위협과 프레임워크별 취약점 대처 가이드.
- [[bun-cpp-addon-compatibility-limits]]: JavaScriptCore와 V8 엔진 차이에 따른 C++ 네이티브 모듈 비호환성 해결 및 안전망 설계 패턴.

## 프로필 반영 후보 (저위험)
- **React2Shell 취약점 조치 기법**: RSC Flight 프로토콜 역직렬화 공격 기전을 이해하고 Next.js 등 프레임워크 패키지 긴급 보안 패치를 수행하는 역량.
- **Bun 환경 표준 모니터링 아키텍처**: V8에 직접 결합된 모니터링 도구 대신 OpenTelemetry 표준 프로토콜(OTLP)로 전환하여 옵저버빌리티를 구성하는 설계 트렌드.

## 승인 필요 (고위험)

## 신규 도구 후보 (에이전트/스킬)
- [agent] wiki-linter — 위키 디렉터리 내 고아 노트(백링크 0), 깨진 위키링크, YAML frontmatter의 요약 필드 누락 및 `status: ai-curated` 속성을 정기 검사하여 구조적 무결성을 유지하는 린터 에이전트.
