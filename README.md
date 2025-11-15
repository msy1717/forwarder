# Telegram Issue Monitor Bot

## Overview
An advanced Telegram bot built with Telethon that monitors multiple groups for specific keywords and automatically forwards detected issues to a centralized alert group. Perfect for community management, customer support, and issue tracking.

## Features
- 🔍 **Multi-Group Monitoring** - Monitor unlimited Telegram groups simultaneously
- 🔑 **Keyword Detection** - Configure custom keywords with categories (e.g., "unstaking" → UNSTAKING_ISSUE)
- 📢 **Auto-Forwarding** - Automatically forwards messages containing keywords to your alert group
- 🏷️ **Issue Categorization** - Tag forwarded messages with custom categories
- 💬 **Interactive Setup** - Uses Telethon conversations for easy configuration
- 🛡️ **Admin-Only Commands** - Secure admin-only access to all management commands
- 💾 **Persistent Storage** - Configuration saved in JSON for persistence across restarts
- 🔤 **Case Sensitivity Toggle** - Enable/disable case-sensitive keyword matching

## Setup Instructions

### 1. Get Telegram API Credentials
1. Visit https://my.telegram.org
2. Log in with your phone number
3. Go to "API development tools"
4. Create a new application
5. Copy your `api_id` and `api_hash`

### 2. Configure Environment Variables
1. Copy `.env.example` to `.env`
2. Fill in your credentials:
   ```
   API_ID=your_api_id_here
   API_HASH=your_api_hash_here
   ADMIN_ID=your_telegram_user_id_here
   SESSION_NAME=issue_monitor_bot
   ```

### 3. Get Your Telegram User ID
- Start the bot (it will guide you through getting your ID)
- Or use [@userinfobot](https://t.me/userinfobot) on Telegram

### 4. Run the Bot
```bash
python main.py
```

## Bot Commands

### Keyword Management
- `/addkeyword <keyword> <category>` - Add a keyword to monitor
  - Example: `/addkeyword unstaking UNSTAKING_ISSUE`
  - Example: `/addkeyword "cannot claim" CLAIM_ERROR`
- `/removekeyword <keyword>` - Remove a keyword from monitoring
- `/listkeywords` - Display all configured keywords and categories

### Group Management
- `/addgroup` - Add the current group to monitoring (use in group)
- `/removegroup` - Remove the current group from monitoring
- `/listgroups` - List all monitored groups
- `/setalert` - Set the current group as the alert/destination group

### Other Commands
- `/start` - Show welcome message and quick start guide
- `/help` - Display all available commands
- `/stats` - Show bot statistics (keywords, groups, status)
- `/togglecase` - Toggle case-sensitive keyword matching

## How It Works

1. **Setup Alert Group** - Create a Telegram group for receiving alerts and use `/setalert` in it
2. **Add Keywords** - Define keywords you want to monitor (e.g., "unstaking", "error", "failed")
3. **Monitor Groups** - Add the bot to groups you want to monitor and use `/addgroup` in each
4. **Automatic Detection** - Bot scans all messages in monitored groups for your keywords
5. **Auto-Forward** - When keywords are detected, the full message is forwarded to your alert group with:
   - Category tags (e.g., [UNSTAKING_ISSUE])
   - Source group name
   - Sender information
   - Timestamp
   - Original message content
   - Direct link to the original message

## Example Workflow

```
1. Create "Issues Hub" group → use /setalert
2. Add keywords:
   /addkeyword unstaking UNSTAKING_ISSUE
   /addkeyword "cannot claim" CLAIM_ERROR
   /addkeyword withdrawal WITHDRAWAL_ISSUE
3. Add bot to community groups → use /addgroup in each
4. Bot automatically forwards matching messages to Issues Hub
```

## Configuration File
The bot stores configuration in `config.json`:
```json
{
  "keywords": {
    "unstaking": "UNSTAKING_ISSUE",
    "cannot claim": "CLAIM_ERROR"
  },
  "monitored_groups": [-1001234567890],
  "alert_group_id": -1009876543210,
  "case_sensitive": false
}
```

## Recent Changes
- **2025-11-15**: Initial bot implementation with all core features

## Project Architecture
- `main.py` - Main bot application with all functionality
- `config.json` - Persistent configuration storage (auto-generated)
- `.env` - Environment variables for API credentials
- Telethon session files - Auto-generated authentication data

## Security Notes
- Never share your `.env` file or session files
- Keep your `API_ID` and `API_HASH` private
- Only the configured admin can use bot commands
- Session files contain authentication tokens - protect them

## Dependencies
- Python 3.11+
- Telethon (Telegram client library)
- python-dotenv (environment variable management)

## User Preferences
- Advanced Python bot implementation
- Using Telethon with conversation API
- Interactive configuration using `await conv.get_response()`
