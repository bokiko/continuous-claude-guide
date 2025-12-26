# Continuous-Claude Complete Installation Guide

> **A step-by-step guide for setting up Continuous-Claude with Claude Code CLI**  
> Supports: **macOS**, **Ubuntu/Debian**, and **Fedora/RHEL**  
> Last Updated: December 2024

---

## Table of Contents

1. [What is Continuous-Claude?](#what-is-continuous-claude)
2. [Part 1: Check Prerequisites](#part-1-check-prerequisites)
3. [Part 2: Install Continuous-Claude](#part-2-install-continuous-claude)
4. [Part 3: Configure Settings](#part-3-configure-settings)
5. [Part 4: Set Up Your Project Workspace](#part-4-set-up-your-project-workspace)
6. [Part 5: Create a Convenient Alias](#part-5-create-a-convenient-alias-optional)
7. [Part 6: Start Using Continuous-Claude](#part-6-start-using-continuous-claude)
8. [Quick Start - Ubuntu](#quick-start---ubuntu)
9. [Quick Start - macOS](#quick-start---macos)
10. [Quick Start - Fedora](#quick-start---fedora)
11. [Available Commands](#available-commands-reference)
12. [Troubleshooting](#troubleshooting)
13. [Uninstall](#uninstall)

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

**macOS:**
```bash
brew install node
```

**Ubuntu/Debian:**
```bash
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
sudo apt-get install -y nodejs
```

**Fedora/RHEL:**
```bash
sudo dnf install nodejs
```

---

### Step 1.3: Check Python

```bash
python3 --version
```

**Expected output:** `Python 3.11.x` or higher (3.9+ may work but 3.11+ recommended)

❌ **If too old or not installed:**

**macOS:**
```bash
brew install python@3.12
```

**Ubuntu 22.04+:**
```bash
sudo apt update
sudo apt install -y python3 python3-venv python3-pip
```

**Ubuntu 20.04 (needs newer Python):**
```bash
sudo add-apt-repository ppa:deadsnakes/ppa
sudo apt update
sudo apt install -y python3.11 python3.11-venv
```

**Fedora/RHEL:**
```bash
sudo dnf install python3.12
```

---

### Step 1.4: Check Git

```bash
git --version
```

**Expected output:** `git version 2.x.x`

❌ **If not installed:**

**macOS:**
```bash
brew install git
```

**Ubuntu/Debian:**
```bash
sudo apt update
sudo apt install -y git
```

**Fedora/RHEL:**
```bash
sudo dnf install git
```

---

### Step 1.5: Check SQLite3

```bash
sqlite3 --version
```

**Expected output:** `3.x.x`

❌ **If not installed:**

**macOS:** Pre-installed ✅

**Ubuntu/Debian:**
```bash
sudo apt install -y sqlite3
```

**Fedora/RHEL:**
```bash
sudo dnf install sqlite
```

---

### Step 1.6: Check jq (JSON Processor)

```bash
jq --version
```

**Expected output:** `jq-1.x`

❌ **If not installed:**

**macOS:**
```bash
brew install jq
```

**Ubuntu/Debian:**
```bash
sudo apt install -y jq
```

**Fedora/RHEL:**
```bash
sudo dnf install jq
```

---

### Step 1.7: Check curl

```bash
curl --version
```

**Expected output:** `curl 7.x.x` or `curl 8.x.x`

❌ **If not installed:**

**Ubuntu/Debian:**
```bash
sudo apt install -y curl
```

**Fedora/RHEL:**
```bash
sudo dnf install curl
```

---

## Part 2: Install Continuous-Claude

### Step 2.1: Open Terminal

- **macOS:** Open Terminal app (Applications → Utilities → Terminal)
- **Ubuntu:** Press `Ctrl + Alt + T` or search for "Terminal"
- **Fedora:** Press `Ctrl + Alt + T` or search for "Terminal"

---

### Step 2.2: Navigate to Your Projects Folder

**macOS:**
```bash
mkdir -p ~/Documents/github
cd ~/Documents/github
```

**Ubuntu/Linux:**
```bash
mkdir -p ~/projects
cd ~/projects
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

This command works on macOS, Ubuntu, and Fedora:

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

**macOS (zsh):**
```bash
source ~/.zshrc
```

**Ubuntu/Debian (bash):**
```bash
source ~/.bashrc
```

**Fedora (bash):**
```bash
source ~/.bashrc
```

---

### Step 2.7: Verify uv Installation

```bash
uv --version
```

**Expected output:** `uv 0.x.x` or similar

❌ **If command not found, add to PATH:**

```bash
export PATH="$HOME/.local/bin:$PATH"
```

Then add this line to your `~/.bashrc` or `~/.zshrc` permanently.

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

This will install to: /home/yourusername/.claude

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
cd ~/path/to/your/project
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

---

**Step 4.2: Set ownership**

**macOS:**
```bash
sudo chown $(whoami):staff /opt/claude-admin
```

**Ubuntu/Debian:**
```bash
sudo chown $(whoami):$(whoami) /opt/claude-admin
```

**Fedora/RHEL:**
```bash
sudo chown $(whoami):$(whoami) /opt/claude-admin
```

---

**Step 4.3: Navigate to the workspace**

```bash
cd /opt/claude-admin
```

---

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

**macOS (zsh):**
```bash
echo 'alias sysadmin="cd /opt/claude-admin && claude"' >> ~/.zshrc
```

**Ubuntu/Debian (bash):**
```bash
echo 'alias sysadmin="cd /opt/claude-admin && claude"' >> ~/.bashrc
```

**Fedora (bash):**
```bash
echo 'alias sysadmin="cd /opt/claude-admin && claude"' >> ~/.bashrc
```

---

### Step 5.2: Reload Your Shell

**macOS:**
```bash
source ~/.zshrc
```

**Ubuntu/Debian/Fedora:**
```bash
source ~/.bashrc
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

## Quick Start - Ubuntu

Copy and paste these commands one section at a time:

### Install Prerequisites

```bash
# Update package list
sudo apt update

# Install required packages
sudo apt install -y git curl sqlite3 jq python3 python3-venv python3-pip

# Install Node.js 20
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
sudo apt-get install -y nodejs

# Verify installations
node --version
python3 --version
git --version
```

### Install Continuous-Claude

```bash
# Create projects folder and clone
mkdir -p ~/projects
cd ~/projects
git clone https://github.com/parcadei/Continuous-Claude.git
cd Continuous-Claude

# Install uv
curl -LsSf https://astral.sh/uv/install.sh | sh
source ~/.bashrc

# Run installer
./install-global.sh

# Configure (minimal - no external services)
echo 'TRACE_TO_BRAINTRUST="false"' > ~/.claude/.env
```

### Set Up Workspace

```bash
# Create admin workspace
sudo mkdir -p /opt/claude-admin
sudo chown $(whoami):$(whoami) /opt/claude-admin

# Initialize project
cd /opt/claude-admin
~/.claude/scripts/init-project.sh

# Add alias for quick access
echo 'alias sysadmin="cd /opt/claude-admin && claude"' >> ~/.bashrc
source ~/.bashrc
```

### Start Using

```bash
# Start Claude
sysadmin

# Then inside Claude, type:
# /continuity_ledger
```

---

## Quick Start - macOS

Copy and paste these commands one section at a time:

### Install Prerequisites

```bash
# Install Homebrew if not installed
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# Install required packages
brew install node python@3.12 git jq

# Verify installations
node --version
python3 --version
git --version
```

### Install Continuous-Claude

```bash
# Create folder and clone
mkdir -p ~/Documents/github
cd ~/Documents/github
git clone https://github.com/parcadei/Continuous-Claude.git
cd Continuous-Claude

# Install uv
curl -LsSf https://astral.sh/uv/install.sh | sh
source ~/.zshrc

# Run installer
./install-global.sh

# Configure (minimal - no external services)
echo 'TRACE_TO_BRAINTRUST="false"' > ~/.claude/.env
```

### Set Up Workspace

```bash
# Create admin workspace
sudo mkdir -p /opt/claude-admin
sudo chown $(whoami):staff /opt/claude-admin

# Initialize project
cd /opt/claude-admin
~/.claude/scripts/init-project.sh

# Add alias for quick access
echo 'alias sysadmin="cd /opt/claude-admin && claude"' >> ~/.zshrc
source ~/.zshrc
```

### Start Using

```bash
# Start Claude
sysadmin

# Then inside Claude, type:
# /continuity_ledger
```

---

## Quick Start - Fedora

Copy and paste these commands one section at a time:

### Install Prerequisites

```bash
# Install required packages
sudo dnf install -y git curl sqlite jq python3 python3-pip nodejs

# Verify installations
node --version
python3 --version
git --version
```

### Install Continuous-Claude

```bash
# Create projects folder and clone
mkdir -p ~/projects
cd ~/projects
git clone https://github.com/parcadei/Continuous-Claude.git
cd Continuous-Claude

# Install uv
curl -LsSf https://astral.sh/uv/install.sh | sh
source ~/.bashrc

# Run installer
./install-global.sh

# Configure (minimal - no external services)
echo 'TRACE_TO_BRAINTRUST="false"' > ~/.claude/.env
```

### Set Up Workspace

```bash
# Create admin workspace
sudo mkdir -p /opt/claude-admin
sudo chown $(whoami):$(whoami) /opt/claude-admin

# Initialize project
cd /opt/claude-admin
~/.claude/scripts/init-project.sh

# Add alias for quick access
echo 'alias sysadmin="cd /opt/claude-admin && claude"' >> ~/.bashrc
source ~/.bashrc
```

### Start Using

```bash
# Start Claude
sysadmin

# Then inside Claude, type:
# /continuity_ledger
```

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

Reinstall uv and add to PATH:

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
export PATH="$HOME/.local/bin:$PATH"
```

**Ubuntu/Fedora:**
```bash
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

**macOS:**
```bash
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.zshrc
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

**macOS:**
```bash
sudo chown -R $(whoami):staff /opt/claude-admin
```

**Ubuntu/Fedora:**
```bash
sudo chown -R $(whoami):$(whoami) /opt/claude-admin
```

---

### Hooks not executing

Make hooks executable:
```bash
chmod +x ~/.claude/hooks/*.sh
```

---

### "bad substitution" error

Don't copy multiple commands at once. Run each command one at a time.

---

### Ubuntu: "add-apt-repository: command not found"

Install software-properties-common:
```bash
sudo apt install -y software-properties-common
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
cd /opt/claude-admin
rm -rf thoughts/
rm -rf .claude/
```

---

## Need Help?

- **GitHub Repository:** https://github.com/parcadei/Continuous-Claude
- **Claude Code Docs:** https://docs.anthropic.com/claude-code

---

*Guide created: December 2024*  
*Supports: macOS, Ubuntu/Debian, and Fedora/RHEL*
