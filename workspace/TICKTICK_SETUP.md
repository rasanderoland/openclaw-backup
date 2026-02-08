# TickTick OAuth Setup Guide for OpenClaw

Complete guide to set up TickTick with full reminder support via ticktick-py.

## Prerequisites

- TickTick account (free or premium)
- OpenClaw installed and running
- Environment variables configured

## Step 1: Register OAuth App with TickTick

### 1.1 Access Developer Portal

Navigate to: **https://developer.ticktick.com**
Log in with your TickTick credentials.

### 1.2 Create New App

Click **"New App"** or **"Register Application"**

Fill in:
- **App Name**: `OpenClaw Integration` (or whatever you prefer)
- **App Description**: `Personal automation via OpenClaw`
- **App Icon**: Optional

### 1.3 Configure OAuth Settings

After creating the app, you'll receive:
- **Client ID** (save this)
- **Client Secret** (save this)

Set the **Redirect URI**: `http://localhost:8080`

## Step 2: Configure Environment Variables

Add to `~/.openclaw/.env`:

```bash
# TickTick OAuth Credentials
TICKTICK_CLIENT_ID="your_client_id_here"
TICKTICK_CLIENT_SECRET="your_client_secret_here"
TICKTICK_REDIRECT_URI="http://localhost:8080"

# Username (for backup auth if needed)
TICKTICK_USERNAME="your@email.com"
TICKTICK_PASSWORD="your_password"
```

## Step 3: Run OAuth Setup

### 3.1 Start SSH Tunnel (if connecting remotely)

If OpenClaw is running on a remote server:

```bash
ssh -L 8080:localhost:8080 user@your-server-ip
```

### 3.2 Initialize OAuth

```bash
python3 ~/.npm-global/lib/node_modules/openclaw/skills/ticktick/ticktick.py
```

This will:
1. Open a web browser for TickTick login
2. Authorize the OAuth app
3. Save tokens to `~/.ticktick-venv/.token-oauth`

### 3.3 Verify Setup

```bash
# List tasks
python3 ~/.npm-global/lib/node_modules/openclaw/skills/ticktick/ticktick.py tasks

# List projects
python3 ~/.npm-global/lib/node_modules/openclaw/skills/ticktick/ticktick.py projects
```

## Step 4: Create Tasks with Reminders

### Basic Task
```bash
python3 ~/.npm-global/lib/node_modules/openclaw/skills/ticktick/ticktick.py create --title "Buy milk"
```

### Task with Due Date
```bash
python3 ~/.npm-global/lib/node_modules/openclaw/skills/ticktick/ticktick.py create --title "Meeting" --due "2024-01-15 14:00"
```

### Task with Reminder
```bash
python3 ~/.npm-global/lib/node_modules/openclaw/skills/ticktick/ticktick.py create --title "Call mom" --reminder "2024-01-15 09:00"
```

## Step 5: Manage Tasks

### Complete a Task
```bash
python3 ~/.npm-global/lib/node_modules/openclaw/skills/ticktick/ticktick.py complete --id "task_id_here"
```

### Delete a Task
```bash
python3 ~/.npm-global/lib/node_modules/openclaw/skills/ticktick/ticktick.py delete --id "task_id_here"
```

## Troubleshooting

### "503 Service Temporarily Unavailable"

TickTick's servers may be temporarily down. Wait a few minutes and retry.

### Token Expired

Delete the cached token and re-authenticate:

```bash
rm ~/.ticktick-venv/.token-oauth
python3 ~/.npm-global/lib/node_modules/openclaw/skills/ticktick/ticktick.py
```

### Port Already in Use

If port 8080 is busy, change the redirect URI in both:
1. TickTick Developer Portal
2. `~/.openclaw/.env` (TICKTICK_REDIRECT_URI)
3. Re-run setup

## Notes

- Tokens are cached in `~/.ticktick-venv/.token-oauth`
- Tokens typically expire after 6 months
- The ticktick-py library handles token refresh automatically
