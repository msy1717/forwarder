# 🚀 Telegram Issue Monitor Bot - Setup Guide

## Authentication Method: USER ACCOUNT (Session Files)

This bot uses **Telethon with session files** to act as your user account. This gives it full access to monitor groups.

---

## Step 1: Get API Credentials

### Visit https://my.telegram.org
1. Log in with your phone number
2. Go to **"API development tools"**
3. Create a new application with any name (e.g., "Issue Monitor")
4. Copy these values:
   - **api_id** (number like `12345678`)
   - **api_hash** (string like `abc123def456...`)

---

## Step 2: Get Your Telegram User ID

### Option A: Use @userinfobot
1. Open Telegram
2. Search for `@userinfobot`
3. Start the bot - it will show your ID

### Option B: Let the bot detect it
Leave `ADMIN_ID` blank in the `.env` file and the bot will detect it automatically on first run.

---

## Step 3: Create .env File

Create a file named `.env` in your project directory:

```bash
# Required: Get from https://my.telegram.org
API_ID=12345678
API_HASH=abc123def456789

# Your Telegram user ID (from @userinfobot)
ADMIN_ID=987654321

# Session file name (can be anything)
SESSION_NAME=issue_monitor_bot
```

**IMPORTANT:** Never share these credentials or commit the `.env` file to GitHub!

---

## Step 4: First Time Login

### Run the bot:
```bash
python main.py
```

### You'll be prompted to:
1. **Enter your phone number** (with country code, e.g., `+1234567890`)
2. **Enter the verification code** sent to your Telegram app
3. **Enter 2FA password** (if you have one enabled)

### What happens:
- Telethon creates a session file: `issue_monitor_bot.session`
- This file stores your authentication
- You won't need to log in again (unless you delete this file)

---

## Step 5: Configure the Bot in Telegram

Once running, configure via Telegram commands:

### 1️⃣ Set Alert Group
```
Create a group for alerts → Add the bot → Use /setalert
```

### 2️⃣ Add Keywords
```
/addkeyword unstaking UNSTAKING_ISSUE
/addkeyword "cannot claim" CLAIM_ERROR
/addkeyword withdrawal WITHDRAWAL_ISSUE
```

### 3️⃣ Add Groups to Monitor
```
Add bot to each group you want to monitor → Use /addgroup
```

---

## ❌ What NOT to Use

### DON'T use Bot Token (@BotFather)
- Bot tokens are for different type of bots
- They can't see all messages in groups (privacy mode limitations)
- They can't act as a user account
- This bot needs user-level access

### DON'T use String Session (unless you know what you're doing)
- String sessions are just portable session files
- File-based sessions (what we use) are simpler and safer
- Only use string sessions if you need to move the bot between servers

---

## 🔒 Security Notes

### Protect These Files:
- `.env` - Contains your API credentials
- `*.session` - Contains your login session
- `*.session-journal` - Session temporary files

### Never:
- Share session files (anyone can access your account)
- Commit `.env` or session files to GitHub
- Share your API_ID or API_HASH publicly
- Give your session files to others

### The .gitignore file already protects:
```
.env
*.session
*.session-journal
config.json
```

---

## 🆘 Troubleshooting

### "API_ID and API_HASH must be set in .env file"
- Make sure you created a `.env` file (not `.env.txt`)
- Check that API_ID and API_HASH are filled in
- API_ID should be a number (no quotes)
- API_HASH should be a string

### "Phone number is not registered"
- Use your Telegram account's phone number
- Include country code (e.g., `+1234567890`)

### "Session file is corrupted"
- Delete the `.session` files
- Run the bot again and log in fresh

### Bot can't see messages in groups
- Make sure the bot is added as a member (not just admin)
- Check that you're using session files (not bot token)
- Privacy mode shouldn't affect user accounts

---

## ✅ Quick Checklist

Before running:
- [ ] Created account on https://my.telegram.org
- [ ] Got API_ID and API_HASH
- [ ] Got your Telegram User ID
- [ ] Created `.env` file with all credentials
- [ ] Ready to enter phone number when prompted

After first run:
- [ ] Logged in successfully
- [ ] Session file created
- [ ] Used `/setalert` in alert group
- [ ] Added keywords with `/addkeyword`
- [ ] Added bot to groups and used `/addgroup`

---

## 📚 Further Reading

- [Telethon Documentation](https://docs.telethon.dev/)
- [How to get API credentials](https://core.telegram.org/api/obtaining_api_id)
- [Telethon Session Files](https://docs.telethon.dev/en/stable/concepts/sessions.html)
