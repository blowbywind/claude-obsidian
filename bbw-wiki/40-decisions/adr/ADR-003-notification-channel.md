---
title: "ADR-003: Hermes 알림 채널 설정"
id: "ADR-003"
status: "proposed"
created: 2026-06-13
updated: 2026-06-13
deciders: [bbw]
supersedes: ""
superseded_by: ""
---

## 맥락

Phase 4 자동화(P4-1~P4-8)가 사용자에게 알림을 보내기 위해 최소 채널 1개 필요.
P0-3 완료 후 `hermes-dashboard` 단독 운영 중. 현재 알림 채널 미설정.

**접근 경로**: `https://snowball.me.kr:9119/` (Caddy → hermes-dashboard:19119)

## 결정

**Phase 4 시작 전까지 결정 보류. 현재는 `pending`.**

우선순위:
1. **Hermes Dashboard** (현재 운영 중) — 수동 확인
2. **Telegram bot** — 사용자가 이동 중에도 알림 수신 가능
3. 이메일 — 보조 채널

## 이유

Phase 1~3 진행 중에 알림 채널 필요성이 구체화됨.
Telegram 설정은 bot token과 chat_id 필요 — 현재 미보유.
Dashboard는 이미 동작 중이므로 Phase 4 시작 전 Telegram 결정.

### 고려한 대안

| 대안 | 장점 | 단점 | 상태 |
|------|------|------|------|
| Hermes Dashboard | 이미 동작 | 브라우저 접속 필요 | 임시 사용 중 |
| Telegram bot | 실시간·모바일 | bot token 설정 필요 | 검토 중 |
| 이메일 | 범용 | 실시간성 낮음 | 보조 |

## 결과

- Phase 4 착수 시점에 채널 1개 이상 확정 필수
- 채널 확정 후 이 ADR을 `accepted`로 업데이트

## 준수 기준

```bash
# Hermes Dashboard 접근 확인
curl -sk https://snowball.me.kr:9119/ | head -5

# Telegram 설정 확인 (설정 후)
docker exec hermes-dashboard hermes status 2>/dev/null | grep -i telegram
```
