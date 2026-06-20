# Settings Parity 보고서: 2026-06-13

> 상태: ⚠️ 불일치
> Claude deny: 23개 | Codex deny: 17개

## 불일치 항목

Claude에만 있는 deny 규칙 (23개):
  - Bash(crontab:*)
  - Bash(dd:*)
  - Bash(git push --force:*)
  - Bash(git push:*)
  - Bash(git reset --hard:*)
  - Bash(npm publish:*)
  - Bash(pnpm publish:*)
  - Bash(rm -rf:*)
  - Bash(ssh-keygen:*)
  - Bash(systemctl:*)
  - Read(**/*.key)
  - Read(**/*.pem)
  - Read(**/.credentials*)
  - Read(**/.env)
  - Read(**/.env.development)
  - Read(**/.env.local)
  - Read(**/.env.production)
  - Read(**/.env.staging)
  - Read(**/.env.test)
  - Read(**/secrets/**)
  - Read(~/.aws/*)
  - Read(~/.config/gcloud/*)
  - Read(~/.ssh/*)

Codex에만 있는 deny 규칙 (17개):
  - **/*.key
  - **/*.p12
  - **/*.pem
  - **/*.pfx
  - **/.credentials*
  - **/.env
  - **/.env.*
  - **/id_ed25519
  - **/id_rsa
  - **/secrets
  - **/secrets/**
  - ~/.aws
  - ~/.claude/.credentials.json
  - ~/.config/gcloud
  - ~/.gemini/google_accounts.json
  - ~/.gemini/oauth_creds.json
  - ~/.ssh

> 필요 시 두 설정을 동기화하세요.
