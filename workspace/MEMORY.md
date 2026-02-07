# MEMORY.md — OpenClaw Long-Term Memory

_Last updated: 2026-02-07_

## User Profile

- **Name:** Gustaf
- **Timezone:** UTC
- **Communication:** Telegram (ID: 7964555583)
- **Telegram bot:** @rasandeclawbot
- **Telegram Groups:** Multiple unnamed groups for different topics
- **Main Group ID:** `-1003751731882`
- **Group Config:** `requireMention: false`, `groupPolicy: "open"`, `allowFrom: [7964555583]`
- **Behavior:** Responds to ALL messages without needing mentions (only two members)
- **Language:** Swedish or English only (no other languages)

## Today's Session (2026-02-07)

### Telegram Pairing Issue Resolved
- **Problem:** Bot showed "not authorized" error
- **Root cause:** User Telegram account not paired with bot
- **Solution:** `openclaw pairing approve telegram 34LY9N57`
- **Pairing code:** 34LY9N57 (Telegram ID: 7964555583)
- **Command:** `openclaw pairing approve telegram <code>`

### Telegram Group Auto-Reply Config
- **Group ID:** `-1003751731882`
- **Config:** 
  - `groupPolicy: "open"` - all senders allowed
  - `requireMention: false` - respond to all messages
  - `allowFrom: [7964555583]` - only approved sender (Gustaf)
- **Purpose:** Auto-reply in groups without needing mentions

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

### Backup Configuration (2026-02-07 Updated)

#### What Gets Backed Up
| Path | Description |
|------|-------------|
| `workspace/` | Agent workspace (MEMORY.md, memory/, etc.) |
| `agents/` | Agent configuration |
| `canvas/` | Canvas UI files |
| `completions/` | Shell completions (bash, fish, ps1, zsh) |
| `cron/` | Scheduled jobs and run history |
| `devices/` | Paired/pending devices |
| `identity/` | Device authentication |
| `telegram/` | Telegram channel state |
| `update-check.json` | Update check metadata |
| `openclaw.json` | Main OpenClaw configuration |

#### What's Excluded (Never Backed Up)
| Path | Reason |
|------|--------|
| `.env` | Contains API keys and passwords |
| `credentials/` | Sensitive authentication files |
| `browser/` | Chrome user data |
| `media/` | Telegram media cache |
| `sessions/` | Active session data |
| `*.log` | Log files |
| `node_modules/` | Dependencies |

#### Backup Process
```bash
# Script location
~/.openclaw/auto-backup.sh

# How it works
1. Rsync copies configured directories to ~/.openclaw-backup/
2. Git commit with timestamp: "Backup: YYYY-MM-DD HH:MM"
3. Force push to GitHub main branch

# Schedule (cron)
0 * * * * ~/.openclaw/auto-backup.sh  # Every hour at minute 0

# Commands
~/.openclaw/auto-backup.sh  # Manual run
crontab -l                  # View schedule
```

#### GitHub Repository
- **URL:** https://github.com/rasanderoland/openclaw-backup
- **Branch:** main
- **Auth:** Via GitHub CLI or PAT token

#### Manual Commands
```bash
# Run backup manually
~/.openclaw/auto-backup.sh

# Check backup repo status
cd ~/.openclaw-backup && git status

# Force push to GitHub
cd ~/.openclaw-backup && git push origin main --force
```

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

### Daily Review
- **Script:** `~/.openclaw/daily-review.js`
- **Schedule:** Daily at 09:00 (cron: `0 9 * * *`)
- **Log:** `~/.openclaw/daily-review.log`
- **Reports:** `~/.openclaw/workspace/memory/review-YYYY-MM-DD.md`
- **Checks:** MEMORY.md, TASKS.md, AGENTS.md, SOUL.md, USER.md, TOOLS.md, HEARTBEAT.md

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
| `~/.openclaw/sync-tasks.js` | GitHub Project sync script |
| `~/.openclaw/update-tasks.js` | GitHub Issues update script |
| `~/.npm-global/lib/node_modules/openclaw/skills/ticktick/` | TickTick skill |
| `~/.config/gogcli/credentials.json` | gog CLI creds |

## Skills

### TickTick Skill
- **Location:** `~/.npm-global/lib/node_modules/openclaw/skills/ticktick/`
- **Purpose:** Full task management in TickTick
- **Status:** Created with full CRUD support
- **Features:**
  - List tasks (filter by project/status)
  - Create tasks with due dates and reminders
  - Edit tasks (title, due date, reminder)
  - Complete tasks
  - Delete tasks
  - Move tasks between projects
- **Usage:**
```bash
# List tasks
ticktick tasks --status pending

# Create task with due date and reminder
ticktick create --title "Buy milk" --project "Shopping" --due "2024-01-15" --reminder "2024-01-15 09:00"

# Edit task
ticktick edit --id 123456789 --title "New title" --due "2024-01-20"

# Complete task
ticktick complete --id 123456789

# Delete task
ticktick delete --id 123456789

# Move to project
ticktick move --id 123456789 --project "Work"
```

## Security Rules

1. **NEVER** paste `.env` contents in chat
2. **NEVER** commit credentials to git
3. Use `${VAR_NAME}` syntax in config files
4. Backup excludes: `.env`, `credentials/`, `*.log`, `sessions/`

## Todo

- [ ] Verify QMD indexing works
- [ ] Test Google Drive for Obsidian vault
- [ ] Confirm backup push to GitHub working
