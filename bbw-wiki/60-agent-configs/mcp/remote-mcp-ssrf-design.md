---
title: Remote MCP/OAuth SSRF 방어 설계
generated: 2026-06-13
phase: P3-4
status: accepted
risks: [R14, R15]
---

# Remote MCP/OAuth SSRF 방어 설계

> P3-4 완료 기준: 7개 방어 항목 포함 설계 문서

Remote MCP 또는 OAuth 도입 전에 완료해야 하는 보안 설계 문서.  
실제 구현 전 이 문서를 검토 기준으로 삼는다.

---

## 방어 항목 1: Private IP / Cloud Metadata URL 차단

**위협**: SSRF를 통해 내부 네트워크(`169.254.169.254`, `10.x.x.x` 등) 또는  
cloud metadata endpoint 접근 시도.

**구현 필수 사항**:
```javascript
// ❌ 라이브러리 수준 블로킹만으로 부족 (octal/hex 우회 가능):
//   octal:  http://0177.0.0.1/  → 127.0.0.1 (localhost)
//   hex:    http://0x7f000001/  → 127.0.0.1
//   decimal:http://2130706433/  → 127.0.0.1

// ✅ URL 파싱 후 numeric IP 직접 검사
import { URL } from "node:url";
import dns from "node:dns/promises";

const BLOCKED_CIDRS = [
  { start: 0x7f000000, end: 0x7fffffff },  // 127.0.0.0/8 (loopback)
  { start: 0xa9fea9fe, end: 0xa9feffff },  // 169.254.0.0/16 (link-local, IMDS)
  { start: 0x0a000000, end: 0x0affffff },  // 10.0.0.0/8 (private)
  { start: 0xac100000, end: 0xac1fffff },  // 172.16.0.0/12 (private)
  { start: 0xc0a80000, end: 0xc0a8ffff },  // 192.168.0.0/16 (private)
  { start: 0xe0000000, end: 0xefffffff },  // 224.0.0.0/4 (multicast)
];

function ipToInt(ip) {
  return ip.split(".").reduce((acc, octet) => (acc << 8) | parseInt(octet, 10), 0) >>> 0;
}

async function isSafeUrl(rawUrl) {
  const parsed = new URL(rawUrl);

  // numeric IP 정규화 (octal/hex/decimal → dotted decimal)
  const hostname = parsed.hostname;
  if (/^[\d.oOxX]+$/.test(hostname)) {
    // node URL이 이미 정규화하므로 parsed.hostname을 재파싱
    const numeric = ipToInt(hostname);
    if (BLOCKED_CIDRS.some(({ start, end }) => numeric >= start && numeric <= end)) {
      return false;
    }
  }

  // DNS 해석 후 결과 IP도 검사 (DNS rebinding 대응)
  try {
    const { address } = await dns.lookup(hostname);
    const numeric = ipToInt(address);
    if (BLOCKED_CIDRS.some(({ start, end }) => numeric >= start && numeric <= end)) {
      return false;
    }
  } catch {
    return false; // 해석 실패 → 거부
  }

  // IPv6 추가 차단 (::1, fc00::/7, fe80::/10)
  if (parsed.hostname.includes(":")) return false;

  return true;
}
```

**차단 대상 URL 예시**:
- `http://169.254.169.254/latest/meta-data/` (AWS IMDS)
- `http://metadata.google.internal/` (GCP 메타데이터)
- `http://0177.0.0.1/` (octal localhost)
- `http://0x7f000001/` (hex localhost)
- `http://2130706433/` (decimal localhost)

---

## 방어 항목 2: HTTPS 강제 (HTTP redirect 거부)

**위협**: HTTP로 시작해 내부 redirect를 통해 private endpoint 접근.

```javascript
// HTTPS만 허용, HTTP redirect 거부
function validateScheme(url) {
  const parsed = new URL(url);
  if (parsed.protocol !== "https:") {
    throw new Error(`HTTPS 필수: ${url}`);
  }
}

// fetch 시 redirect: "error" 또는 수동 검증
const res = await fetch(url, {
  redirect: "manual",  // redirect 수동 처리
});
if (res.status >= 300 && res.status < 400) {
  const location = res.headers.get("location");
  if (!location || !(await isSafeUrl(location))) {
    throw new Error(`안전하지 않은 redirect: ${location}`);
  }
  // redirect URL도 HTTPS·private IP 재검증
  validateScheme(location);
  // 최대 redirect 횟수 제한 (예: 3회)
}
```

---

## 방어 항목 3: Redirect 검증 (Open Redirect 차단)

**위협**: 정상 MCP 서버가 악성 URL로 redirect → open redirect 경유 SSRF.

**구현**:
- redirect chain 전체를 재검증 (각 Location 헤더마다 `isSafeUrl()` 적용)
- 최대 redirect 횟수: 3회 초과 시 거부
- 다른 origin으로의 redirect 금지 (같은 도메인만 허용 옵션)

```javascript
async function safeFetch(url, maxRedirects = 3) {
  let current = url;
  let count = 0;
  while (count <= maxRedirects) {
    if (!(await isSafeUrl(current))) throw new Error(`SSRF 차단: ${current}`);
    const res = await fetch(current, { redirect: "manual" });
    if (res.status < 300 || res.status >= 400) return res;
    const loc = res.headers.get("location");
    if (!loc) throw new Error("Location 헤더 없음");
    current = new URL(loc, current).href; // 상대 redirect 해소
    count++;
  }
  throw new Error(`redirect 횟수 초과 (${maxRedirects})`);
}
```

---

## 방어 항목 4: MCP Server 전용 Token Audience 검증

**위협**: 클라이언트 bearer token을 MCP 서버로 전달(passthrough)하면  
token audience 검증 없이 임의 서버가 클라이언트 권한으로 작동.

**구현**:
```javascript
// JWT audience 클레임 검증
import jwt from "jsonwebtoken";

function validateTokenAudience(token, expectedAudience) {
  const decoded = jwt.decode(token, { complete: true });
  if (!decoded) throw new Error("JWT 파싱 실패");

  const { aud } = decoded.payload;
  const audiences = Array.isArray(aud) ? aud : [aud];

  if (!audiences.includes(expectedAudience)) {
    throw new Error(
      `token audience 불일치: expected=${expectedAudience}, got=${audiences.join(",")}`
    );
  }
}

// 사용 예: MCP 서버별 고유 audience 설정
const MCP_SERVER_AUDIENCE = "mcp:obsidian-gateway:snowball.me.kr";
validateTokenAudience(incomingToken, MCP_SERVER_AUDIENCE);
```

**원칙**: MCP 서버마다 고유 audience (`mcp:<server-id>:<host>`) 사용.

---

## 방어 항목 5: Token Passthrough 방지

**위협**: Claude Code 또는 Codex의 API 토큰이 MCP 서버 요청 헤더에 그대로 전달  
→ 악성 MCP 서버가 API 토큰 탈취 가능.

**구현 원칙**:
- MCP 서버에는 **전용 서비스 토큰**만 발급 (Claude/Codex API 토큰 공유 금지)
- `Authorization: Bearer <claude-api-key>` 헤더를 MCP 서버로 전달 금지
- MCP 서버 인증: OAuth 2.0 Client Credentials (서버 전용 scope)
- token 저장: 메모리 또는 전용 secrets store (환경변수 직접 전달 금지)

```
# 금지 패턴
MCP_TOKEN=$ANTHROPIC_API_KEY node mcp-server.js  # ❌ passthrough

# 허용 패턴
MCP_TOKEN=$(get-mcp-service-token) node mcp-server.js  # ✅ 전용 토큰
```

---

## 방어 항목 6: OAuth Scope 최소화

**위협**: 과도한 OAuth scope → 침해 시 피해 범위 확대.

**원칙**:
- 초기 요청: `mcp:tools-basic` (기본 도구 목록 조회만)
- 권한 상승 필요 시: `WWW-Authenticate` challenge → 사용자 명시적 승인
- write scope: `mcp:obsidian:write` (게이트웨이 경유만 허용)
- 절대 금지: `mcp:*` 또는 와일드카드 scope

```
# OAuth scope 계층 예시
mcp:tools-basic       — tools/list 조회만
mcp:obsidian:read     — obsidian 읽기
mcp:obsidian:write    — obsidian append-only write (gateway 필수)
mcp:repo:read         — /home/bbw/projects 읽기
mcp:admin             — 절대 미사용 (운영자 전용 API key 별도)
```

---

## 방어 항목 7: DNS Rebinding 방어

**위협**: MCP 서버 DNS가 검증 시점(A 레코드 확인)과 실제 연결 시점 사이에  
private IP로 변경 → 방어 우회.

**구현**:
- DNS 조회 결과를 요청 수명 동안 캐시 (TTL 무시, 고정)
- 연결 시점에서도 IP 재검증 (`socket` 이벤트 또는 `connect` 훅)
- 또는: IP 직접 지정 + TLS SNI 분리 (가장 강력)

```javascript
// Node.js http.Agent로 연결 후 IP 재검증
const agent = new https.Agent({
  lookup: async (hostname, options, callback) => {
    const { address, family } = await dns.lookup(hostname);
    if (!(await isSafeUrl(`http://${address}/`))) {
      return callback(new Error(`DNS rebinding 차단: ${address}`));
    }
    callback(null, address, family);
  },
});
```

---

## 체크리스트 (Remote MCP 도입 전 필수)

- [ ] 방어 항목 1 구현: numeric IP 검사 (`isSafeUrl()`)
- [ ] 방어 항목 2 구현: HTTPS 강제 + HTTP redirect 거부
- [ ] 방어 항목 3 구현: redirect chain 전체 재검증, 최대 3회
- [ ] 방어 항목 4 구현: `audience` 클레임 검증 (MCP 서버별 전용)
- [ ] 방어 항목 5 구현: API 토큰 passthrough 방지, 전용 서비스 토큰
- [ ] 방어 항목 6 구현: OAuth scope 최소화, `mcp:tools-basic`에서 시작
- [ ] 방어 항목 7 구현: DNS rebinding 방어 (lookup 훅 또는 IP 고정)

> ⚠️ Remote MCP를 도입하기 전에 위 7개 항목이 모두 체크되어야 한다.
