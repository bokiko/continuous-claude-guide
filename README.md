# Continuous-Claude Installation Guide

> **Context management system for Claude Code CLI**  
> Maintains session state, handoffs, and learnings across Claude Code sessions.

---

## Table of Contents

1. [Overview](#overview)
2. [Prerequisites](#prerequisites)
3. [Installation](#installation)
4. [Configuration](#configuration)
5. [Project Setup](#project-setup)
6. [Usage](#usage)
7. [Available Commands](#available-commands)
8. [API Keys Reference](#api-keys-reference)
9. [Troubleshooting](#troubleshooting)
10. [Uninstallation](#uninstallation)

---

## Overview

### What is Continuous-Claude?

Continuous-Claude is a context management system that helps Claude Code CLI "remember" your work across sessions. It provides:

| Feature | Description |
|---------|-------------|
| **Continuity Ledger** | Tracks session state, goals, and progress |
| **Handoffs** | Creates documents to transfer context between sessions |
| **Session Tracing** | Logs actions to Braintrust for analysis (optional) |
| **Auto-Learnings** | Extracts insights from sessions to improve future work |
| **MCP Tools** | Adds web search, scraping, and documentation tools |

### Who Should Use This?

- ✅ Claude Code CLI users working on long-running projects
- ✅ Developers who need context persistence across sessions
- ✅ Teams wanting session analytics and learning extraction

### Compatibility

| Platform | Compatible |
|----------|------------|
| Claude Code CLI | ✅ Yes |
| Cursor IDE | ❌ No |
| VS Code + Claude Extension | ❌ No |

---

## Prerequisites

### Required Software

```bash
# 1. Claude Code CLI (must be installed and working)
claude --version
# Expected: Claude Code v1.x.x or higher

# 2. Node.js (v18+ recommended)
node --version
# Expected: v18.x.x or higher

# 3. Python (3.11+ recommended)
python3 --version
# Expected: Python 3.11.x or higher

# 4. Git
git --version
# Expected: git version 2.x.x

# 5. SQLite3
sqlite3 --version
# Expected: 3.x.x
```

### Optional Software

```bash
# jq - JSON processor (used by some hooks)
brew install jq  # macOS
# or: apt install jq  # Linux
```

---

## Installation

### Step 1: Clone the Repository

```bash
# Navigate to your preferred directory
cd ~/Documents/github  # or any directory you prefer

# Clone the repository
git clone https://github.com/parcadei/Continuous-Claude.git

# Enter the directory
cd Continuous-Claude
```

### Step 2: Install uv (Python Package Manager)

**Option A: Official installer (recommended)**
```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

**Option B: Via pip**
```bash
pip install uv
```

**Option C: Via Homebrew (macOS)**
```bash
brew install uv
```

After installation, reload your shell:
```bash
source ~/.zshrc  # for Zsh
# or
source ~/.bashrc  # for Bash
```

Verify installation:
```bash
uv --version
```

### Step 3: Install qlty (Code Quality Tool) - Optional

**Option A: Official installer**
```bash
curl -fsSL https://qlty.sh/install.sh | bash
```

**Option B: Skip this step**
- qlty is optional and only used for code quality checks
- The installer will attempt to install it automatically

### Step 4: Run the Global Installer

```bash
# Make sure you're in the Continuous-Claude directory
cd ~/Documents/github/Continuous-Claude

# Run the installer
./install-global.sh
```

The installer will:
1. Create a backup of your existing `~/.claude/` directory
2. Install skills, agents, rules, and hooks to `~/.claude/`
3. Set up MCP configuration
4. Create necessary cache directories

**Expected output:**
```
┌─────────────────────────────────────────────────────────────┐
│  Continuous Claude - Global Installation                    │
└─────────────────────────────────────────────────────────────┘

This will install to: /Users/you/.claude

Creating full backup at ~/.claude-backup-20251226_120000...
Backup complete.

Copying skills...
Copying agents...
Copying rules...
Copying hooks...
Copying scripts...
Copying MCP config...

Installation complete!
```

---

## Configuration

### Step 1: Create Environment File

```bash
# Create or edit the environment file
nano ~/.claude/.env
```

### Step 2: Add API Keys

Add the following to `~/.claude/.env`:

```bash
# ═══════════════════════════════════════════════════════════════
# CONTINUOUS-CLAUDE CONFIGURATION
# ═══════════════════════════════════════════════════════════════

# ─────────────────────────────────────────────────────────────────
# SESSION TRACING (Optional but recommended)
# ─────────────────────────────────────────────────────────────────
# Enable/disable Braintrust session tracing
TRACE_TO_BRAINTRUST="false"  # Set to "true" to enable

# Braintrust API key (get from https://braintrust.dev)
# BRAINTRUST_API_KEY="sk-..."

# ─────────────────────────────────────────────────────────────────
# OPTIONAL SERVICES (Add keys for services you want to use)
# ─────────────────────────────────────────────────────────────────

# Perplexity AI - Web search (https://perplexity.ai/settings/api)
# PERPLEXITY_API_KEY="pplx-..."

# Firecrawl - Web scraping (https://firecrawl.dev)
# FIRECRAWL_API_KEY="fc-..."

# GitHub - Code search (https://github.com/settings/tokens)
# GITHUB_PERSONAL_ACCESS_TOKEN="ghp_..."

# Morph - Fast code search (https://morphllm.com)
# MORPH_API_KEY="sk-..."

# Nia - Library documentation (https://trynia.ai)
# NIA_API_KEY="nk_..."
```

### Step 3: Minimal Configuration (No External Services)

If you just want the core features without external services:

```bash
echo 'TRACE_TO_BRAINTRUST="false"' > ~/.claude/.env
```

This gives you:
- ✅ Continuity ledgers
- ✅ Handoffs
- ✅ Plans
- ✅ Local artifact indexing
- ❌ Session tracing (disabled)
- ❌ Web search (no API key)

---

## Project Setup

### Initialize Each Project

For every project you want to use with Continuous-Claude:

```bash
# Navigate to your project
cd /path/to/your/project

# Run the project initializer
~/.claude/scripts/init-project.sh
```

### What Gets Created

```
your-project/
├── thoughts/
│   ├── ledgers/              ← Continuity ledger files
│   │   └── CONTINUITY_CLAUDE-<session>.md
│   └── shared/
│       ├── handoffs/         ← Session handoff documents
│       │   └── <session>/
│       │       └── task-01.md
│       └── plans/            ← Implementation plans
│           └── 2025-01-15-feature-name.md
├── .claude/
│   └── cache/
│       └── artifact-index/
│           └── context.db    ← Local SQLite search index
└── .gitignore                ← Updated to ignore .claude/cache/
```

### Verify Setup

```bash
# Check that directories were created
ls -la thoughts/
ls -la .claude/cache/artifact-index/
```

---

## Usage

### Starting a Session

```bash
# Navigate to your initialized project
cd /path/to/your/project

# Start Claude Code CLI
claude
```

### Creating a Continuity Ledger

On your first session, create a ledger to track your work:

```
You: /continuity_ledger

Claude: I'll create a continuity ledger for this session...
        [Creates thoughts/ledgers/CONTINUITY_CLAUDE-<session>.md]
```

### Creating a Handoff

When ending a session or switching tasks:

```
You: /create_handoff

Claude: I'll create a handoff document...
        [Creates thoughts/shared/handoffs/<session>/task-XX.md]
```

### Resuming Work

When starting a new session:

```
You: /resume_handoff

Claude: Loading previous session context...
        [Reads the latest handoff and continues where you left off]
```

---

## Available Commands

### Core Commands

| Command | Description |
|---------|-------------|
| `/continuity_ledger` | Create/update session tracking ledger |
| `/create_handoff` | Save current work state for next session |
| `/resume_handoff` | Resume from previous session's handoff |
| `/create_plan` | Create an implementation plan |
| `/implement_plan` | Execute a plan using TDD |
| `/implement_task` | Implement a specific task |

### Research & Search Commands

| Command | Description | Requires |
|---------|-------------|----------|
| `/perplexity-search` | AI-powered web search | PERPLEXITY_API_KEY |
| `/github-search` | Search GitHub code/issues | GITHUB_PERSONAL_ACCESS_TOKEN |
| `/firecrawl-scrape` | Scrape web pages | FIRECRAWL_API_KEY |
| `/nia-docs` | Search library documentation | NIA_API_KEY |
| `/morph-search` | Fast codebase search | MORPH_API_KEY |

### Analysis Commands

| Command | Description | Requires |
|---------|-------------|----------|
| `/braintrust-analyze` | Analyze session traces | BRAINTRUST_API_KEY |
| `/qlty-check` | Run code quality checks | qlty installed |
| `/ast-grep-find` | AST-based code search | ast-grep installed |

### Development Commands

| Command | Description |
|---------|-------------|
| `/commit` | Create a git commit with generated message |
| `/describe_pr` | Generate PR description |
| `/debug` | Debug an issue with structured approach |
| `/research` | Research a topic |

---

## API Keys Reference

### Where to Get API Keys

| Service | URL | Free Tier |
|---------|-----|-----------|
| Braintrust | https://braintrust.dev | ✅ Yes |
| Perplexity | https://perplexity.ai/settings/api | ✅ Limited |
| Firecrawl | https://firecrawl.dev | ✅ Limited |
| GitHub | https://github.com/settings/tokens | ✅ Yes |
| Morph | https://morphllm.com | ❓ Check site |
| Nia | https://trynia.ai | ❓ Check site |

### Recommended Setup

**Minimal (free, no external services):**
```bash
TRACE_TO_BRAINTRUST="false"
```

**Basic (with session tracing):**
```bash
TRACE_TO_BRAINTRUST="true"
BRAINTRUST_API_KEY="sk-..."
```

**Full (all features):**
```bash
TRACE_TO_BRAINTRUST="true"
BRAINTRUST_API_KEY="sk-..."
PERPLEXITY_API_KEY="pplx-..."
GITHUB_PERSONAL_ACCESS_TOKEN="ghp_..."
```

---

## Troubleshooting

### Common Issues

#### "Command not found: uv"
```bash
# Reinstall uv
curl -LsSf https://astral.sh/uv/install.sh | sh
source ~/.zshrc
```

#### "No ledger found" warning
```bash
# Initialize your project first
~/.claude/scripts/init-project.sh

# Then create a ledger in Claude
# /continuity_ledger
```

#### Hooks not working
```bash
# Check if hooks are executable
ls -la ~/.claude/hooks/

# Make them executable if needed
chmod +x ~/.claude/hooks/*.sh
```

#### "Database not found" error
```bash
# Re-initialize your project
~/.claude/scripts/init-project.sh
```

#### Session tracing not working
```bash
# Check your .env file
cat ~/.claude/.env

# Make sure these are set:
# TRACE_TO_BRAINTRUST="true"
# BRAINTRUST_API_KEY="sk-..."
```

### Checking Logs

```bash
# Braintrust hook logs
cat ~/.claude/state/braintrust_hook.log

# Learning extraction logs
cat ~/.claude/cache/learn.log
```

---

## Uninstallation

### Option 1: Restore Backup

```bash
# Find your backup
ls -la ~/.claude-backup-*

# Remove current installation
rm -rf ~/.claude

# Restore backup
mv ~/.claude-backup-YYYYMMDD_HHMMSS ~/.claude
```

### Option 2: Complete Removal

```bash
# Remove global installation
rm -rf ~/.claude

# Remove project-specific files (in each project)
cd /path/to/your/project
rm -rf thoughts/
rm -rf .claude/cache/
```

### Option 3: Keep Configuration, Remove Tools

```bash
# Keep your .env file
cp ~/.claude/.env ~/claude-env-backup.txt

# Remove installation
rm -rf ~/.claude

# Create minimal .claude directory
mkdir -p ~/.claude
mv ~/claude-env-backup.txt ~/.claude/.env
```

---

## Quick Reference Card

```
┌─────────────────────────────────────────────────────────────┐
│  CONTINUOUS-CLAUDE QUICK REFERENCE                          │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  SETUP:                                                     │
│    git clone https://github.com/parcadei/Continuous-Claude  │
│    cd Continuous-Claude && ./install-global.sh              │
│    cd your-project && ~/.claude/scripts/init-project.sh    │
│                                                             │
│  START SESSION:                                             │
│    cd your-project && claude                                │
│                                                             │
│  KEY COMMANDS:                                              │
│    /continuity_ledger  - Start tracking session             │
│    /create_handoff     - Save work for next session         │
│    /resume_handoff     - Continue previous work             │
│    /create_plan        - Create implementation plan         │
│                                                             │
│  CONFIG FILE:                                               │
│    ~/.claude/.env                                           │
│                                                             │
│  LOGS:                                                      │
│    ~/.claude/state/braintrust_hook.log                      │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

---

## Additional Resources

- **GitHub Repository**: https://github.com/parcadei/Continuous-Claude
- **Claude Code CLI Docs**: https://docs.anthropic.com/claude-code
- **Braintrust**: https://braintrust.dev

---

*Guide created: December 2024*  
*For Continuous-Claude with Claude Code CLI*

