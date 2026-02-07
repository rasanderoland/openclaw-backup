# OpenClaw Tasks & Projects

_Last updated: 2026-02-07 19:55_

_Source: GitHub Project (github.com/users/rasanderoland/projects/1)_

## Overview

**Total:** 4 open, 1 closed

---

## Tasks (from GitHub Project)

### Open Tasks

| Task |
|------|
| [Integrate Google Workspace CLI (gog) for Gmail/Calendar/Drive](https://github.com/rasanderoland/openclaw-tasks/issues/2) |
| [Integrate Bitwarden for password management](https://github.com/rasanderoland/openclaw-tasks/issues/3) |
| [Integrate Perplexity for web search](https://github.com/rasanderoland/openclaw-tasks/issues/6) |
| [Integrate TickTick for task management](https://github.com/rasanderoland/openclaw-tasks/issues/1) |

### Completed Tasks

| Task |
|------|
| [Set up Discord channel monitoring](https://github.com/rasanderoland/openclaw-tasks/issues/4) |


---

## Local Notes

### In Progress
- QMD memory backend fully operational (vector embeddings working)
- Daily review script created for automatic file checks

### Completed Today (2026-02-07)
- ✅ Telegram pairing issue resolved (pairing code: 34LY9N57)
- ✅ QMD backend enabled with citations
- ✅ Backup system fixed with auto-push to GitHub
- ✅ Chrome cleanup script added (frees ~1.6 GB RAM)
- ✅ IPv6 fix for Telegram (NODE_OPTIONS=ipv4first)
- ✅ TickTick skill created with full CRUD (create, edit, complete, delete, move)
- ✅ Daily review script created (checks MEMORY.md, TASKS.md, AGENTS.md, etc.)
- ✅ USER.md updated with Gustaf's profile
- ✅ GitHub Project sync established (synctasks.js)

### Pending
- Test TickTick skill with real API credentials
- Update MEMORY.md with daily notes (Telegram pairing already documented)

---

## Commands

```bash
# Daily review
node ~/.openclaw/daily-review.js

# Sync tasks from GitHub
node ~/.openclaw/sync-tasks.js

# Update GitHub issues
node ~/.openclaw/update-tasks.js

# Manual backup
~/.openclaw/auto-backup.sh

# Cleanup Chrome (every 6 hours)
~/.openclaw/cleanup-chrome.sh
```

## References

- **GitHub Project:** https://github.com/users/rasanderoland/projects/1
- **Backup Repo:** https://github.com/rasanderoland/openclaw-backup
- **Logs:** /tmp/openclaw/openclaw-2026-02-07.log
