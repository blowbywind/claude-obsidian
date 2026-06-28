---
type: bot-artifact
bot: rina
runtime: antigravity
source: /home/bbw/.gemini/antigravity-cli/brain/37a0ddd6-ed4e-4d61-97a2-4eb8075d2594/autobots_design_audit.md
session: 37a0ddd6-ed4e-4d61-97a2-4eb8075d2594
harvested_at: 2026-06-27T04:03:38.704Z
summary: "Detailed UI/UX design audit report for the Autobots project. Analyzes visual consistency, responsive layout structures, and accessibility/contrast issues, offering actionable refactoring code patterns to clean up inline hardcoded styles into semantic CSS/Tailwind v4 variables."
---
# Autobots UI/UX 디자인 점검 보고서 (Design & Layout Audit)

이 보고서는 **리나(UI/UX 디자이너)**의 관점에서 `Autobots` 프로젝트 프론트엔드의 디자인 일관성, 반응형 레이아웃, 그리고 화면 정보 가독성(가시성)을 다각도로 진단하고 개선 방향을 제시한 디자인 점검 문서입니다.

---

## 1. 디자인 일관성 및 토큰 활용성 점검 (Visual Consistency)

### 🟢 강점 (Strengths)
* **체계적인 3계층 토큰 설계**: [globals.css](file:///home/bbw/ai-ops/autobots/frontend/app/globals.css) 내에 Primitive ➔ Semantic ➔ Component 계층 구조의 CSS 변수 토큰이 올바르게 설계되어 있습니다.
* **Modern CSS-first 테마**: Tailwind CSS v4의 `@theme inline` 구조 및 CSS native `light-dark()` 함수를 사용하여, 운영체제/브라우저 테마 설정을 기반으로 한 유연한 라이트/다크모드 지원 구조를 확립했습니다.
* **Base UI + Tailwind v4 매핑**: 컴포넌트 내에서 `@base-ui/react` 및 `data-slot` 스타일링 패턴을 활용하여 최신 프론트엔드 표준을 준수하고 있습니다.

### 🔴 취약점 (Weaknesses)
* **Hex 색상 코드의 하드코딩과 인라인 스타일 남용**:
  * [page.tsx](file:///home/bbw/ai-ops/autobots/frontend/app/page.tsx), [settings/page.tsx](file:///home/bbw/ai-ops/autobots/frontend/app/settings/page.tsx), [TwoPanel.tsx](file:///home/bbw/ai-ops/autobots/frontend/components/TwoPanel.tsx) 등 주요 파일 곳곳에 `#E0D9CF` (Sand-400), `#F5F0EB` (Sand-100), `#FCEEE7` (Clay-50), `#C44020` (Clay-500) 등 디자인 토큰에 정의된 프리미티브 색상들이 `style={{ border: '1px solid #E0D9CF' }}` 등의 형태로 인라인 하드코딩되어 있습니다.
* **다크 모드 미호환성**:
  * 인라인으로 고정된 배경색(`background: '#F5F0EB'`)이나 보더 색상이 적용되어 있을 경우, 다크 모드 실행 시 배경 및 보더가 어두워지지 않고 그대로 유지됩니다. 이로 인해 다크 모드 텍스트 컬러(밝은 색)와 결합되어 화면을 알아볼 수 없는 **눈부심 및 가독성 불일치**가 야기됩니다.
  * `RosterChip`의 `background: '#fff'` 역시 다크 모드에서 검은 배경 위에 흰 칩이 지나치게 대비되거나 가독성을 해치는 원인이 됩니다.

---

## 2. 반응형 디자인 및 레이아웃 점검 (Responsive Layout)

### 🟢 강점 (Strengths)
* **터치 타깃 및 줌 방지 (Mobile-first UX)**:
  * 모바일 화면(767px 이하) 터치 시 브라우저가 입력을 강제로 확대(Zoom-in)하지 않도록 입력 폼들의 글자 크기를 `16px !important`로 선언하여 모바일 입력 사용성을 확보했습니다.
* **레이아웃 붕괴 방지**:
  * 메인 대시보드의 `StatCard` 슬라이더(`overflow-x-auto flex-nowrap sm:grid`)는 모바일에서 가로 스크롤로, 데스크톱에서는 4열 그리드로 변경되는 모던 그리드 방식을 차용하고 있습니다.
  * [TwoPanel.tsx](file:///home/bbw/ai-ops/autobots/frontend/components/TwoPanel.tsx)가 모바일에서는 `flex-col`로 붕괴되고, 데스크톱 이상에서 `md:flex-row`와 고정폭(`--lw`) 레이아웃을 통해 가로 2단 패널로 확장되는 설계가 매끄럽게 동작합니다.
* **사이드바 토글 인터랙션**:
  * 모바일 화면 대응용 오버레이 및 `-translate-x-full`과 `lg:translate-x-0` 트랜지션을 사용하여 사이드바 진입/이탈이 자연스러우며, `Escape` 키 입력 감지 및 ARIA 명세가 준수되어 웹 접근성(A11y) 기준이 높습니다.

### 🔴 취약점 (Weaknesses)
* **인라인 크기 지정**:
  * [TopBar.tsx](file:///home/bbw/ai-ops/autobots/frontend/components/TopBar.tsx)와 [Sidebar.tsx](file:///home/bbw/ai-ops/autobots/frontend/components/Sidebar.tsx)에 `style={{ height: '44px' }}` 및 `style={{ width: '186px' }}`과 같은 고정 크기 제어가 하드코딩되어 있어, 유동적인 레이아웃 변형 및 Tailwind 유틸리티 조율 시 유연성을 저해할 수 있습니다.

---

## 3. 화면 가독성 및 정보 가시성 점검 (Contrast & Accessibility)

### 🟢 강점 (Strengths)
* **고해상도 다국어 타이포그래피**:
  * Pretendard 웹폰트를 최상위 글로벌 스타일에 임포트하여, 다양한 디바이스 환경에서 한글 가독성 및 영문 서체 렌더링이 매우 미려하고 정교합니다.
* **모션 및 스크롤 감쇠 대응**:
  * 스크롤바 커스텀 스타일 및 윈도우 애니메이션 감축 미디어 쿼리(`prefers-reduced-motion`)가 선언되어 모션 멀미 등을 예방하여 WCAG 2.2 AA 사용성을 충족합니다.

### 🔴 취약점 (Weaknesses)
* **텍스트 최소 크기 및 명암비(Contrast Ratio)**:
  * 대시보드 화면에 `text-[11px]`, `text-[12px]` 크기의 보조 텍스트가 밀도 높게 모여 있습니다.
  * 특히 `#F5F0EB`의 밝은 회색 바탕에 `text-muted-foreground`가 얹혀진 경우, 명암비가 낮아져 저시력자나 야외 모바일 환경에서 텍스트 가시성이 심각하게 저해됩니다 (WCAG 2.2 AA 기준, 본문 텍스트 최소 4.5:1 이상 명암비 확보 필요).
* **커스텀 툴팁 포지셔닝 구조**:
  * `RosterChip` 내부의 마우스 호버형 툴팁 포지셔닝이 JavaScript 기반 상태(`tip`)와 인라인 절대 좌표(`position: 'absolute'`)로 설계되어 있어, 스크롤 영역 끝에 가 있거나 뷰포트 크기가 작을 때 툴팁 내용이 화면 밖으로 벗어나는 **Obscure(포커스 가려짐)** 위험이 있습니다.

---

## 4. 구체적인 코드 개선 제안 (Actionable Code Improvements)

### 🛠️ 제안 1. 하드코딩된 인라인 스타일 제거 및 Tailwind v4 토큰화
다크 모드와 테마 시스템이 완벽하게 동기화되도록, 각 파일의 하드코딩 Hex 스타일 코드를 Tailwind v4 클래스로 변경합니다.

```diff
// 1. TwoPanel.tsx (CSS 테두리 토큰화)
-        style={{
-          borderRight: '1px solid #E0D9CF',
-          borderBottom: '1px solid #E0D9CF',
-        }}
+        className="w-full md:shrink-0 flex flex-col overflow-y-auto bg-card border-b md:border-b-0 md:border-r border-border"

// 2. app/page.tsx (대시보드 패널 카드 테두리 및 배경)
-          <div className="rounded-lg bg-card flex flex-col lg:flex-1" style={{ border: '1px solid #E0D9CF' }}>
+          <div className="rounded-lg bg-card flex flex-col lg:flex-1 border border-border">

-            <div className="flex items-center justify-between px-5 py-3.5" style={{ borderBottom: '1px solid #E0D9CF' }}>
+            <div className="flex items-center justify-between px-5 py-3.5 border-b border-border">

-                <div className="rounded-lg flex items-center justify-center h-16 text-[12px] text-muted-foreground" style={{ background: '#F5F0EB' }}>
+                <div className="rounded-lg flex items-center justify-center h-16 text-[12px] text-muted-foreground bg-secondary/40">

-                    <div key={item.id} className="flex items-center gap-3 py-2 px-3 rounded-lg" style={{ background: '#F5F0EB' }}>
+                    <div key={item.id} className="flex items-center gap-3 py-2 px-3 rounded-lg bg-secondary/40">

// 3. app/settings/page.tsx (설정 카드 아이콘 배경)
-              <div
-                className="w-9 h-9 rounded-lg flex items-center justify-center shrink-0"
-                style={{ background: '#FCEEE7', color: '#C44020' }}
-              >
+              <div className="w-9 h-9 rounded-lg flex items-center justify-center shrink-0 bg-accent text-accent-foreground">
```

### 🛠️ 제안 2. 가독성을 위한 최소 폰트 조정 및 명암 확보
가독성이 지나치게 떨어지는 `text-[11px]` 사용 구역을 가급적 `text-[12px]` 또는 `text-xs`로 상향하고, 연한 회색 배경에서는 텍스트에 `text-foreground` 또는 `font-semibold` 가중치를 부여해 시인성을 보장합니다.

```diff
// app/page.tsx
-                 <span className="text-[13px] font-semibold text-foreground">오늘의 할 일</span>
-                 <span className="text-[11px] text-muted-foreground ml-2">Today tasks</span>
+                 <span className="text-sm font-semibold text-foreground">오늘의 할 일</span>
+                 <span className="text-xs text-muted-foreground ml-2">Today tasks</span>
```

### 🛠️ 제안 3. CSS Anchor Positioning과 Popover API 우선 도입 검토
`app/chat/page.tsx`의 호버 툴팁과 팝오버를 구현할 때 JavaScript 상태를 통한 복잡한 렌더링 대신, 최신 브라우저가 표준으로 지원하는 CSS Anchor Positioning 및 HTML Popover API를 사용하여 레이아웃 복잡성을 낮추고 보조 기기(ARIA) 호환성을 강화할 수 있습니다.

---
## 요약 권장 사항
1. **1순위**: `app/page.tsx`, `settings/page.tsx`, `TwoPanel.tsx` 등의 인라인 하드코딩 스타일(`style={{ background: '#F5F0EB' }}` 등)을 전면 제거하고, Tailwind의 `bg-secondary` 및 `border-border` 등의 토큰으로 마이그레이션하여 **다크 모드 가독성**을 완벽하게 확보합니다.
2. **2순위**: 11px 수준의 가독성 저해 텍스트를 최하 12px(또는 Tailwind `text-xs`) 이상으로 교정하고, 라이트 모드 상에서의 저명암 대비 영역을 개선합니다.
