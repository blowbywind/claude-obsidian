# 외부 채널 연결 상태 확인 — 2026-06-19

> 갱신: 2026-06-19T11:30Z (autobots-scheduler, scheduled task)

## 요약

- 외부 채널: **5개** (총 24채널 중)
- 백엔드 API: **UP** (port 9200)
- **실제 외부 연결 가능 채널: 0개** — 전체 외부 채널 webhook/url 미설정

## 외부 채널 현황

| 채널 ID | 이름 | DB Status | Webhook | 최근 메시지 |
|---------|------|-----------|---------|------------|
| ch-discord-dev | Discord #dev | active | null | 없음 |
| ch-slack-deploy | Slack #deployments | active | null | 없음 |
| ch-slack-hnedu | Slack #hnedu-alerts | active | null | 없음 |
| ch-tg-alerts | Telegram @alert_bot | active | null | 없음 |
| ch-tg-ops | Telegram @ops_bot | active | null | 없음 |

## 진단

- DB의 status 필드는 모두 active이나 실제 연동에 필요한 webhook URL이 전부 null
- /api/channels/:id/send 호출 시 "webhook not configured" 오류 발생 예정
- 인바운드 수신 엔드포인트(/api/webhooks/in)는 구현됨, 아웃바운드 전송 불가

## 조치 필요

- [ ] Slack webhook URL 발급 후 ch-slack-deploy, ch-slack-hnedu 등록
- [ ] Telegram Bot Token + chat_id 설정
- [ ] Discord Webhook URL 등록 (ch-discord-dev)
- [ ] 등록 후 /api/channels/:id/send 테스트 메시지로 연결 검증

## 내부/프라이빗 채널

- Internal 18개: webhook 불필요, 내부 SSE 방식 사용, 모두 active
- Private 1개: #admin (haeri 봇 담당)
