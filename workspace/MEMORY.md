# MEMORY.md — OpenClaw Long-Term Memory

_Last updated: 2026-02-07_

## User Profile

- **Name:** Gustaf
- **Timezone:** UTC
- **Communication:** Telegram (ID: 7964555583)
- **Telegram bot:** @rasandeclawbot

## Key Decisions & Preferences

### Telegram Configuration
- **Issue:** Bot showed "not authorized" error
- **Solution:** Pair user with `openclaw pairing approve telegram 34LY9N57`
- **Telegram ID:** 7964555583
- **Bot token:** Stored in `.env` as `TELEGRAM_BOT_TOKEN`

### Environment Variables
- All credentials moved from `openclaw.json` to `~/.openclaw/.env`
- Uses `${VAR_NAME}` syntax in config for env var interpolation
- Systemd service loads `EnvironmentFile=/home/rasandeclaw/.openclaw/.env`

### HelloFresh Workflow
- **Cookie-based scraping** (Cloudflare blocks headless)
- **Cookie file:** `/home/rasandeclaw/.openclaw/workspace/hellofresh_cookies.json`
- **Scripts:** `hellofresh-login.js`, `hellofresh-import-scrape.js`
- **Recipes saved:** `/home/rasandeclaw/.openclaw/workspace/hellofresh_recipes.json`
- **Seafood filter:** fish, lax, salmon, torsk, räkor, skaldjur, etc.

### Google Workspace (gog)
- **Account:** rasandeclaw@gmail.com
- **Credentials:** OAuth 2.0 Desktop app (not Service Account)
- **Credentials file:** `~/.config/gogcli/credentials.json`
- **Working:** Gmail, Calendar
- **Pending:** Drive (for Obsidian vault sharing)

### QMD Memory Backend (Experimental)
- **Enabled:** Yes (2026-02-07)
- **Installation:** Bun + `bun install -g https://github.com/tobi/qmd`
- **Config:** `memory.backend = "qmd"` in openclaw.json
- **Location:** `~/.openclaw/agents/main/qmd/`

### Backup Configuration
- **Script:** `~/.openclaw/auto-backup.sh`
- **Schedule:** Hourly (cron: `0 * * * *`)
- **Backup repo:** `~/.openclaw-backup/` (local) → GitHub (pending auth)
- **Remote:** https://github.com/rasanderoland/openclaw-backup.git
- **Excludes:** `.env`, `credentials/`, `*.log`, `sessions/`, `.git/`

## OpenClaw Version & Updates

### Current Version
- **Version:** 2026.2.3-1
- **Latest:** 2026.2.6 (as of 2026-02-07)

### Recent Changes (v2026.2.2 - v2026.2.6)
- xAI (Grok) support added
- Token usage dashboard in Web UI
- Voyage AI for memory embeddings
- Telegram DM topic threadId fix
- Cron scheduling fixes
- Feishu/Lark plugin
- QMD backend support

## Technical Notes

### Systemd Service
- **Service file:** `~/.config/systemd/user/openclaw-gateway.service`
- **Environment:** `EnvironmentFile=/home/rasandeclaw/.openclaw/.env`
- **Status:** `systemctl --user status openclaw-gateway`

### Gateway Configuration
- **Port:** 18789
- **Mode:** local-only (loopback)
- **Auth:** Token-based (`OPENCLAW_GATEWAY_TOKEN`)
- **Logs:** `/tmp/openclaw/openclaw-2026-02-07.log`

### Models
- **Primary:** MiniMax-M2.1 (reasoning enabled)
- **Secondary:** MiniMax-M2.1-lightning (reasoning enabled)
- **Provider:** minimax-portal (OAuth)

## Files & Locations

| Path | Description |
|------|-------------|
| `~/.openclaw/workspace/` | Agent workspace |
| `~/.openclaw/openclaw.json` | Main config |
| `~/.openclaw/.env` | Secrets (NEVER commit) |
| `~/.config/gogcli/credentials.json` | gog CLI credentials |
| `~/.config/systemd/user/openclaw-gateway.service` | Systemd service |
| `~/.openclaw/auto-backup.sh` | Backup script |
| `~/.openclaw-backup/` | Local backup repo |

## Security Rules

1. **NEVER** paste `.env` contents in chat
2. **NEVER** commit credentials to git
3. Use `${VAR_NAME}` syntax in config files
4. Backup excludes: `.env`, `credentials/`, `*.log`, `sessions/`

## Todo / In Progress

- [ ] Set up GitHub auth for backup push (`gh auth login`)
- [ ] Enable Google Drive Obsidian vault sharing
- [ ] Complete QMD setup and verify indexing
- [ ] Test backup push to GitHub
