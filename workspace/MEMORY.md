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

### GitHub Tasks Repository (Kanban Board)
- **Repo:** `rasanderoland/openclaw-tasks`
- **Project ID:** `PVT_kwHODgRTtM4BOmP2`
- **Purpose:** Personal task management via GitHub Issues Kanban board
- **Sync script:** `~/.openclaw/sync-tasks.js`
- **Commands:** `gh issue list/create/view/close --repo rasanderoland/openclaw-tasks`
- **Labels:** `task`, `api`, etc.
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
- **Status:** Created with full OAuth support

### Twitter/X Skill (Browser-Based)
- **Location:** `~/.npm-global/lib/node_modules/openclaw/skills/twitter/`
- **Purpose:** Read-only access to Twitter/X via browser automation
- **Status:** Created (read-only, no posting)
- **Commands:**
  - `twitter timeline [--count N]` - Read home timeline
  - `twitter search "query" [--count N]` - Search tweets
  - `twitter user username [--count N]` - Read user profile
  - `twitter tweet <id>` - View specific tweet
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

### 🔐 CRITICAL: Never Expose Credentials

**GOLDEN RULES:**
1. **NEVER** post credentials in GitHub issues (even private repos)
2. **NEVER** paste `.env` contents in chat
3. **NEVER** commit credentials to git
4. **ALWAYS** use `${VAR_NAME}` syntax in config files, never hardcode values
5. **ALWAYS** revoke and rotate credentials immediately if exposed

### GitHub Issues Security Protocol

**ABSOLUTELY FORBIDDEN in GitHub Issues:**
- API keys/tokens of any kind
- Access tokens (Bearer, OAuth, PAT)
- Usernames + password combinations
- Database connection strings
- Private keys or certificates
- Any secrets from `.env`

**If credentials must be documented:**
- Use placeholders only: `X_API_KEY=${X_API_KEY}`
- Add comment: `# DO NOT FILL IN - Use .env instead`
- Reference external secret manager if needed

### GitHub Token Best Practices

**Token naming convention:**
- `GH_TOKEN` for GitHub PAT (in .env)
- `GITHUB_TOKEN` alternative naming

**Script template:**
```javascript
// ❌ NEVER: const GITHUB_TOKEN = 'ghp_xxxxxxxxxxxx';
// ✅ ALWAYS: const GITHUB_TOKEN = process.env.GH_TOKEN;
```

**Token scopes (minimum required):**
- `repo` - full control of private repos (for sync-tasks.js)
- `read:user` - read user profile data
- Never grant `delete_repo` or `admin:org` unless absolutely required

### Credential Rotation Protocol

If credentials are exposed (even accidentally):
1. **IMMEDIATELY** revoke the credential on the provider's dashboard
2. **IMMEDIATELY** create a new credential with minimum required scope
3. **IMMEDIATELY** update `.env` with new credential
4. **IMMEDIATELY** delete/edit any GitHub issues/comments where credentials appeared
5. **Within 24h** check GitHub's "Exposed secrets" alerts
6. **Document** the incident in MEMORY.md for future reference

---

**INCIDENT 2026-02-08:**
- Issue #10 in `rasanderoland/openclaw-tasks` contained:
  - `X_API_KEY: qicfiE5AupkBgDwUHsKsqHSN1`
  - `X_ACCESS_TOKEN: 94094159-...`
- **Action taken:** Issue deleted, credentials revoked, sync-tasks.js fixed
- **Lesson:** GitHub Issues are NOT secure storage for secrets

### Backup Exclusions
| Path | Reason |
|------|--------|
| `.env` | Contains API keys and passwords |
| `credentials/` | Sensitive authentication files |
| `.git/` | Git history may contain accidentally committed secrets |

## Todo

- [ ] Verify QMD indexing works
- [ ] Test Google Drive for Obsidian vault
- [ ] Confirm backup push to GitHub working
