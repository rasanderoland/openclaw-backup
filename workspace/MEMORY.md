# MEMORY.md — OpenClaw Long-Term Memory

_Last updated: 2026-02-07_

## User Profile

- **Name:** Gustaf
- **Timezone:** UTC
- **Communication:** Telegram (ID: 7964555583)
- **Telegram bot:** @rasandeclawbot

## Today's Session (2026-02-07)

### Telegram Pairing Issue Resolved
- **Problem:** Bot showed "not authorized" error
- **Root cause:** User Telegram account not paired with bot
- **Solution:** `openclaw pairing approve telegram 34LY9N57`
- **Pairing code:** 34LY9N57 (Telegram ID: 7964555583)
- **Command:** `openclaw pairing approve telegram <code>`

### QMD Backend Enabled (Experimental)
- **Bun:** Already installed (`/home/rasandeclaw/.bun/bin/bun`, v1.3.8)
- **QMD installed:** `bun install -g https://github.com/tobi/qmd`
- **Config added to openclaw.json:**
  - `memory.backend: "qmd"`
  - `memory.citations: "auto"`
  - QMD runs from `~/.openclaw/agents/main/qmd/`
- **First search may be slow** (downloads GGUF models on first use)

### Thinking Mode Enabled
- MiniMax-M2.1: `reasoning: true`
- MiniMax-M2.1-lightning: `reasoning: true`

### Backup System Fixed
- **Script:** `~/.openclaw/auto-backup.sh`
- **Schedule:** Hourly (cron: `0 * * * *`)
- **Repo:** `~/.openclaw-backup/` → GitHub (force pushed to `main`)
- **Remote:** `https://github.com/rasanderoland/openclaw-backup.git`
- **Excludes:** `.env`, `credentials/`, `*.log`, `sessions/`, `.git/`
- **Auto-push to GitHub:** Enabled in script

### MEMORY.md Recovered
- File was missing (never existed in backup or workspace)
- Recreated with all relevant configuration
- **Pushed to GitHub:** `workspace/MEMORY.md` in master/main branch

## Key Decisions & Preferences

### Environment Variables Migration
- All credentials moved from `openclaw.json` to `~/.openclaw/.env`
- Uses `${VAR_NAME}` syntax in config
- Systemd service: `EnvironmentFile=/home/rasandeclaw/.openclaw/.env`

### HelloFresh Workflow
- **Cookie-based scraping** (Cloudflare blocks headless)
- **Cookie file:** `/home/rasandeclaw/.openclaw/workspace/hellofresh_cookies.json`
- **Scripts:** `hellofresh-login.js`, `hellofresh-import-scrape.js`
- **Recipes saved:** `/home/rasandeclaw/.openclaw/workspace/hellofresh_recipes.json`
- **Seafood filter:** fish, lax, salmon, torsk, räkor, skaldjur, etc.

### Google Workspace (gog)
- **Account:** rasandeclaw@gmail.com
- **Credentials:** OAuth 2.0 Desktop app
- **Working:** Gmail, Calendar
- **Pending:** Drive (Obsidian vault sharing)

## OpenClaw Version & Updates

### Current Version
- **Version:** 2026.2.3-1
- **Latest:** 2026.2.6

### v2026.2.6 Highlights
- xAI (Grok) support
- Token usage dashboard in Web UI
- Voyage AI for memory embeddings
- Telegram DM topic threadId fix
- Cron scheduling fixes
- Feishu/Lark plugin

## Technical Notes

### Systemd Service
- **Service:** `~/.config/systemd/user/openclaw-gateway.service`
- **Status:** `systemctl --user status openclaw-gateway`
- **Logs:** `/tmp/openclaw/openclaw-2026-02-07.log`

### Gateway Config
- **Port:** 18789
- **Mode:** local-only (loopback)
- **Auth:** Token-based

## Files & Locations

| Path | Description |
|------|-------------|
| `~/.openclaw/workspace/` | Agent workspace |
| `~/.openclaw/workspace/MEMORY.md` | Long-term memory |
| `~/.openclaw/workspace/memory/YYYY-MM-DD.md` | Daily notes |
| `~/.openclaw/openclaw.json` | Main config |
| `~/.openclaw/.env` | Secrets (NEVER commit) |
| `~/.openclaw/auto-backup.sh` | Backup script |
| `~/.openclaw-backup/` | Local backup repo |
| `~/.config/gogcli/credentials.json` | gog CLI creds |

## Security Rules

1. **NEVER** paste `.env` contents in chat
2. **NEVER** commit credentials to git
3. Use `${VAR_NAME}` syntax in config files
4. Backup excludes: `.env`, `credentials/`, `*.log`, `sessions/`

## Todo

- [ ] Verify QMD indexing works
- [ ] Test Google Drive for Obsidian vault
- [ ] Confirm backup push to GitHub working
