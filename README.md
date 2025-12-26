# Continuous-Claude Complete Installation Guide

> **A step-by-step guide for setting up Continuous-Claude with Claude Code CLI**  
> Last Updated: December 2024

---

## What is Continuous-Claude?

Continuous-Claude is a **context management system** for Claude Code CLI that helps Claude "remember" your work across sessions.

### Features
- 📝 **Continuity Ledger** - Tracks your session state, goals, and progress
- 🔄 **Handoffs** - Saves your work so you can continue later
- 📊 **Session Tracing** - Logs your sessions for analysis (optional)
- 🧠 **Auto-Learnings** - Extracts insights to improve future sessions
- 🛠️ **Extra Tools** - Web search, code quality checks, and more

### Important
- ✅ Works with: **Claude Code CLI** (terminal command `claude`)
- ❌ Does NOT work with: Cursor IDE, VS Code extensions

---

## Part 1: Check Prerequisites

Open your terminal and run each command to verify you have the required software.

### Step 1.1: Check Claude Code CLI

```bash
claude --version
```

**Expected output:** `2.x.x (Claude Code)` or similar

❌ **If not installed:** Get it from https://docs.anthropic.com/claude-code

---

### Step 1.2: Check Node.js

```bash
node --version
```

**Expected output:** `v18.x.x` or higher

❌ **If not installed:**
```bash
brew install node
```

---

### Step 1.3: Check Python

```bash
python3 --version
```

**Expected output:** `Python 3.11.x` or higher (3.9+ may work but 3.11+ recommended)

❌ **If too old or not installed:**
```bash
brew install python@3.12
```

---

### Step 1.4: Check Git

```bash
git --version
```

**Expected output:** `git version 2.x.x`

❌ **If not installed:**
```bash
brew install git
```

---

### Step 1.5: Check SQLite3

```bash
sqlite3 --version
```

**Expected output:** `3.x.x`

✅ Usually pre-installed on macOS

---

## Part 2: Install Continuous-Claude

### Step 2.1: Open Terminal

Open the Terminal app on your Mac.

---

### Step 2.2: Navigate to Your GitHub Folder

```bash
cd ~/Documents/github
```

**Note:** If this folder doesn't exist, create it:
```bash
mkdir -p ~/Documents/github
cd ~/Documents/github
```

---

### Step 2.3: Clone the Repository

```bash
git clone https://github.com/parcadei/Continuous-Claude.git
```

**Expected output:**
```
Cloning into 'Continuous-Claude'...
remote: Enumerating objects: ...
...
Resolving deltas: 100% ... done.
```

---

### Step 2.4: Enter the Directory

```bash
cd Continuous-Claude
```

---

### Step 2.5: Install uv (Python Package Manager)

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

**Expected output:**
```
Downloading uv...
Installing to ~/.local/bin...
Done!
```

---

### Step 2.6: Reload Your Shell

```bash
source ~/.zshrc
```

**Note:** If you use bash instead of zsh:
```bash
source ~/.bashrc
```

---

### Step 2.7: Verify uv Installation

```bash
uv --version
```

**Expected output:** `uv 0.x.x` or similar

---

### Step 2.8: Run the Global Installer

```bash
./install-global.sh
```

**Expected output:**
```
┌─────────────────────────────────────────────────────────────┐
│  Continuous Claude - Global Installation                    │
└─────────────────────────────────────────────────────────────┘

This will install to: /Users/yourusername/.claude

Creating full backup at ~/.claude-backup-...
Copying skills...
Copying agents...
Copying rules...
Copying hooks...
Copying scripts...
Copying MCP config...
Copying plugins...
Installing settings.json...

Installation complete!
```

✅ **Continuous-Claude is now installed globally!**

---

## Part 3: Configure Settings

### Step 3.1: Open the Configuration File

```bash
nano ~/.claude/.env
```

---

### Step 3.2: Set Minimal Configuration

Delete everything in the file and add this single line:

```
TRACE_TO_BRAINTRUST="false"
```

---

### Step 3.3: Save and Exit

1. Press `Ctrl + X`
2. Press `Y` to confirm save
3. Press `Enter` to confirm filename

---

### Step 3.4: Verify Configuration

```bash
cat ~/.claude/.env
```

**Expected output:**
```
TRACE_TO_BRAINTRUST="false"
```

---

## Part 4: Set Up Your Project Workspace

You need to initialize a project directory where Claude will store session data.

### Option A: For Regular Projects

If you have a specific project (like a coding project):

```bash
cd ~/Documents/github/your-project-name
~/.claude/scripts/init-project.sh
```

---

### Option B: For System Administration (Recommended for Root Access)

If you use Claude to manage system files and network settings:

**Step 4.1: Create the admin workspace**
```bash
sudo mkdir -p /opt/claude-admin
```
Enter your password when prompted.

**Step 4.2: Set ownership (replace `yourusername` with your actual username)**
```bash
sudo chown yourusername:staff /opt/claude-admin
```

**Example for user "bokiko":**
```bash
sudo chown bokiko:staff /opt/claude-admin
```

**Step 4.3: Navigate to the workspace**
```bash
cd /opt/claude-admin
```

**Step 4.4: Initialize the project**
```bash
~/.claude/scripts/init-project.sh
```

**Expected output:**
```
┌─────────────────────────────────────────────────────────────┐
│  Continuous Claude - Project Initialization                 │
└─────────────────────────────────────────────────────────────┘

Project: /opt/claude-admin

Creating directory structure...
Initializing Artifact Index database...
  ✓ Database created at .claude/cache/artifact-index/context.db

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Project initialized! Directory structure:

  thoughts/
  ├── ledgers/           ← Continuity ledgers
  └── shared/
      ├── handoffs/      ← Session handoffs
      └── plans/         ← Implementation plans
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

## Part 5: Create a Convenient Alias (Optional)

This lets you start Claude quickly with a simple command.

### Step 5.1: Add the Alias

**For system admin workspace:**
```bash
echo 'alias sysadmin="cd /opt/claude-admin && claude"' >> ~/.zshrc
```

**For a regular project:**
```bash
echo 'alias myproject="cd ~/Documents/github/your-project && claude"' >> ~/.zshrc
```

---

### Step 5.2: Reload Your Shell

```bash
source ~/.zshrc
```

---

### Step 5.3: Test the Alias

```bash
sysadmin
```

This should open Claude in your workspace!

---

## Part 6: Start Using Continuous-Claude

### Step 6.1: Start Claude

**With alias:**
```bash
sysadmin
```

**Without alias:**
```bash
cd /opt/claude-admin
claude
```

---

### Step 6.2: Create Your First Ledger

Once Claude is running, type:

```
/continuity_ledger
```

Claude will create a ledger file to track your session.

---

### Step 6.3: Work Normally

Use Claude as you normally would. The ledger tracks your progress automatically.

---

### Step 6.4: Save Your Work (Handoff)

When you're done or taking a break, type:

```
/create_handoff
```

Claude will save a summary of your work.

---

### Step 6.5: Resume Later

Next time you start Claude, type:

```
/resume_handoff
```

Claude will load your previous context and continue where you left off.

---

## Available Commands Reference

### Core Commands

| Command | What It Does |
|---------|--------------|
| `/continuity_ledger` | Create/update your session ledger |
| `/create_handoff` | Save your work for later |
| `/resume_handoff` | Continue from last session |
| `/create_plan` | Create an implementation plan |
| `/implement_plan` | Execute a plan step by step |

### Other Useful Commands

| Command | What It Does |
|---------|--------------|
| `/commit` | Create a git commit |
| `/debug` | Debug an issue systematically |
| `/qlty-check` | Run code quality checks |

---

## Troubleshooting

### "Command not found: claude"

Claude Code CLI is not installed. Get it from:
https://docs.anthropic.com/claude-code

---

### "Command not found: uv"

Reinstall uv:
```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
source ~/.zshrc
```

---

### "No ledger found" warning

Initialize your project first:
```bash
cd /your/project/path
~/.claude/scripts/init-project.sh
```

---

### "Permission denied" errors

Make sure you own the project directory:
```bash
sudo chown -R yourusername:staff /opt/claude-admin
```

---

### Hooks not executing

Make hooks executable:
```bash
chmod +x ~/.claude/hooks/*.sh
```

---

## File Locations Reference

| What | Location |
|------|----------|
| Global installation | `~/.claude/` |
| Configuration | `~/.claude/.env` |
| Hooks | `~/.claude/hooks/` |
| Skills | `~/.claude/skills/` |
| Project ledgers | `your-project/thoughts/ledgers/` |
| Project handoffs | `your-project/thoughts/shared/handoffs/` |
| Backup of old config | `~/.claude-backup-YYYYMMDD_HHMMSS/` |

---

## Uninstall

### Remove Global Installation

```bash
rm -rf ~/.claude
```

### Restore Previous Configuration

```bash
# Find your backup
ls ~/.claude-backup-*

# Restore it
mv ~/.claude-backup-YYYYMMDD_HHMMSS ~/.claude
```

### Remove Project Files

```bash
cd /your/project
rm -rf thoughts/
rm -rf .claude/
```

---

## Quick Start Summary

```bash
# 1. Clone
cd ~/Documents/github
git clone https://github.com/parcadei/Continuous-Claude.git
cd Continuous-Claude

# 2. Install uv
curl -LsSf https://astral.sh/uv/install.sh | sh
source ~/.zshrc

# 3. Run installer
./install-global.sh

# 4. Configure (minimal)
echo 'TRACE_TO_BRAINTRUST="false"' > ~/.claude/.env

# 5. Create workspace
sudo mkdir -p /opt/claude-admin
sudo chown yourusername:staff /opt/claude-admin
cd /opt/claude-admin
~/.claude/scripts/init-project.sh

# 6. Add alias
echo 'alias sysadmin="cd /opt/claude-admin && claude"' >> ~/.zshrc
source ~/.zshrc

# 7. Start using!
sysadmin
```

---

## Need Help?

- **GitHub Repository:** https://github.com/parcadei/Continuous-Claude
- **Claude Code Docs:** https://docs.anthropic.com/claude-code

---

*Guide created: December 2024*
