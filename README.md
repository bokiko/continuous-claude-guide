<div align="center">

# Continuous-Claude

<h3>Give Claude Code a memory. Pick up where you left off, every time.</h3>

<p>
  <a href="#quick-start">
    <img src="https://img.shields.io/badge/setup-10%20minutes-success" alt="10 min setup" />
  </a>
  <a href="https://github.com/AnandChowdhary/continuous-claude">
    <img src="https://img.shields.io/badge/based%20on-Continuous--Claude-blue" alt="Based on Continuous-Claude" />
  </a>
  <a href="https://github.com/bokiko/continuous-claude-guide/blob/main/LICENSE">
    <img src="https://img.shields.io/badge/license-MIT-green" alt="MIT License" />
  </a>
</p>

<p>
  <a href="https://bokiko.io">bokiko.io</a> · <a href="https://twitter.com/bokiko">@bokiko</a>
</p>

</div>

---

## Table of Contents

1. [The Problem](#the-problem)
2. [The Solution](#the-solution)
3. [Who is this for?](#who-is-this-for)
4. [How it works](#how-it-works-simple-version)
5. [Quick Start](#quick-start) (Let Claude install it for you!)
6. [Manual Installation](#manual-installation) (macOS, Ubuntu, Fedora)
7. [Commands Reference](#commands-reference)
8. [Companion Tools](#companion-tools)
9. [Custom Statusline](#custom-statusline)
10. [FAQ](#faq)
11. [Troubleshooting](#troubleshooting)
12. [Credits](#credits)

---

## The Problem

Every time you close Claude Code, it forgets everything. Your progress, your decisions, the context you spent 30 minutes building up - gone.

**Sound familiar?**
- "Wait, what were we working on yesterday?"
- "I already explained this architecture to you..."
- "Can you remember what we decided about the database?"

Claude Code is stateless by default. Each session starts fresh. That's fine for quick questions, but terrible for real work.

---

## The Solution

**Continuous-Claude** gives Claude Code persistent memory through:

| Feature | What it does |
|---------|--------------|
| **Continuity Ledger** | Tracks your session state, goals, and progress |
| **Handoffs** | Saves your work so you can continue later |
| **Session Tracing** | Logs your sessions for analysis (optional) |
| **Auto-Learnings** | Extracts insights to improve future sessions |
| **Extra Tools** | Web search, code quality checks, and more |

**The result?** Claude remembers what you were working on, what decisions you made, and where you left off.

---

## Who is this for?

| If you're... | Continuous-Claude helps you... |
|--------------|-------------------------------|
| **Using Claude Code daily** | Stop re-explaining context every session |
| **Working on long projects** | Maintain progress across days/weeks |
| **Managing infrastructure** | Keep runbooks and system knowledge available |
| **Doing complex refactors** | Track multi-step plans without losing state |
| **New to Claude Code** | Build good habits from day one |

---

## How it works (simple version)

**Without Continuous-Claude:**
```
Day 1: "Let's refactor the auth system"
       [Claude learns your codebase, makes progress]
       [Session ends]

Day 2: "Continue the auth refactor"
       Claude: "I don't have any context about an auth refactor.
                Could you explain what you're working on?"
       [Start over from scratch]
```

**With Continuous-Claude:**
```
Day 1: "Let's refactor the auth system"
       [Claude learns your codebase, makes progress]
       [You type: /create_handoff]
       [Session ends]

Day 2: "Continue the auth refactor"
       [You type: /resume_handoff]
       Claude: "I see we completed the JWT migration yesterday.
                Next up is updating the middleware. Ready?"
       [Continue where you left off]
```

---

## Quick Start

### The Easy Way (Recommended)

**Let Claude handle the entire setup for you!** This is the smoothest experience - Claude will install everything, configure it, and verify it works.

Copy and paste this prompt to Claude:

```
I'd like you to set up Continuous-Claude for my Claude Code environment.

Please:
1. Check my OS (macOS/Ubuntu/Fedora) and install any missing prerequisites
2. Clone and install Continuous-Claude from https://github.com/parcadei/Continuous-Claude
3. Run the global installer (install-global.sh)
4. Configure with minimal settings (TRACE_TO_BRAINTRUST="false")
5. Create a workspace at /opt/claude-admin and initialize it
6. Add a convenient alias to my shell config
7. Verify everything is working
8. Give me a quick summary of what was set up and the commands I can use

Start by checking what's already installed on my system.
```

Claude will:
- Detect your operating system
- Install missing dependencies (node, python, git, etc.)
- Clone and configure Continuous-Claude
- Set up your workspace
- Verify the installation works
- Teach you the basic commands

**That's the recommended approach!** Claude handles all the technical details.

---

## Manual Installation

If you prefer to control every step, expand your OS below:

<details>
<summary><strong>macOS Installation</strong></summary>

### Prerequisites

```bash
# Install Homebrew if not installed
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# Install required packages
brew install node python@3.12 git jq

# Verify installations
node --version    # Should be 18+
python3 --version # Should be 3.11+
```

### Install Continuous-Claude

```bash
# Clone the repository
mkdir -p ~/Documents/github && cd ~/Documents/github
git clone https://github.com/parcadei/Continuous-Claude.git
cd Continuous-Claude

# Install uv (Python package manager)
curl -LsSf https://astral.sh/uv/install.sh | sh
source ~/.zshrc

# Run the installer
./install-global.sh

# Configure (minimal - no external services)
echo 'TRACE_TO_BRAINTRUST="false"' > ~/.claude/.env
```

### Set Up Your Workspace

```bash
# Create workspace
sudo mkdir -p /opt/claude-admin
sudo chown $(whoami):staff /opt/claude-admin

# Initialize project
cd /opt/claude-admin
~/.claude/scripts/init-project.sh

# Add quick-start alias
echo 'alias sysadmin="cd /opt/claude-admin && claude"' >> ~/.zshrc
source ~/.zshrc
```

### Start Using

```bash
sysadmin
# Then inside Claude: /continuity_ledger
```

</details>

<details>
<summary><strong>Ubuntu Installation</strong></summary>

### Prerequisites

```bash
# Update and install required packages
sudo apt update
sudo apt install -y git curl sqlite3 jq python3 python3-venv python3-pip

# Install Node.js 20
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
sudo apt-get install -y nodejs

# Verify installations
node --version    # Should be 18+
python3 --version # Should be 3.11+
```

### Install Continuous-Claude

```bash
# Clone the repository
mkdir -p ~/projects && cd ~/projects
git clone https://github.com/parcadei/Continuous-Claude.git
cd Continuous-Claude

# Install uv (Python package manager)
curl -LsSf https://astral.sh/uv/install.sh | sh
source ~/.bashrc

# Run the installer
./install-global.sh

# Configure (minimal - no external services)
echo 'TRACE_TO_BRAINTRUST="false"' > ~/.claude/.env
```

### Set Up Your Workspace

```bash
# Create workspace
sudo mkdir -p /opt/claude-admin
sudo chown $(whoami):$(whoami) /opt/claude-admin

# Initialize project
cd /opt/claude-admin
~/.claude/scripts/init-project.sh

# Add quick-start alias
echo 'alias sysadmin="cd /opt/claude-admin && claude"' >> ~/.bashrc
source ~/.bashrc
```

### Start Using

```bash
sysadmin
# Then inside Claude: /continuity_ledger
```

</details>

<details>
<summary><strong>Fedora Installation</strong></summary>

### Prerequisites

```bash
# Install required packages
sudo dnf install -y git curl sqlite jq python3 python3-pip nodejs

# Verify installations
node --version    # Should be 18+
python3 --version # Should be 3.11+
```

### Install Continuous-Claude

```bash
# Clone the repository
mkdir -p ~/projects && cd ~/projects
git clone https://github.com/parcadei/Continuous-Claude.git
cd Continuous-Claude

# Install uv (Python package manager)
curl -LsSf https://astral.sh/uv/install.sh | sh
source ~/.bashrc

# Run the installer
./install-global.sh

# Configure (minimal - no external services)
echo 'TRACE_TO_BRAINTRUST="false"' > ~/.claude/.env
```

### Set Up Your Workspace

```bash
# Create workspace
sudo mkdir -p /opt/claude-admin
sudo chown $(whoami):$(whoami) /opt/claude-admin

# Initialize project
cd /opt/claude-admin
~/.claude/scripts/init-project.sh

# Add quick-start alias
echo 'alias sysadmin="cd /opt/claude-admin && claude"' >> ~/.bashrc
source ~/.bashrc
```

### Start Using

```bash
sysadmin
# Then inside Claude: /continuity_ledger
```

</details>

---

## Requirements

| Requirement | Version | Check command |
|------------|---------|---------------|
| Claude Code CLI | Any | `claude --version` |
| Node.js | 18+ | `node --version` |
| Python | 3.11+ | `python3 --version` |
| Git | Any | `git --version` |
| SQLite3 | Any | `sqlite3 --version` |
| jq | Any | `jq --version` |
| curl | Any | `curl --version` |

**Important:**
- Works with: **Claude Code CLI** (terminal command `claude`)
- Does NOT work with: Cursor IDE, VS Code extensions

---

## Commands Reference

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

## Companion Tools

### BloxCue - Reduce Token Usage by 90%

Once you have Continuous-Claude set up, add [**BloxCue**](https://github.com/bokiko/bloxcue) to dramatically reduce your token usage.

| Problem | Solution |
|---------|----------|
| Large CLAUDE.md files load on every prompt | BloxCue loads only relevant context blocks |
| ~8,500 tokens wasted per prompt | ~800 tokens loaded (only what's needed) |
| Hit token limits faster | Save ~7,000+ tokens per prompt |

**Quick Install:**
```bash
git clone https://github.com/bokiko/bloxcue.git
cd bloxcue
./install.sh
```

Or just tell Claude: *"Install BloxCue for me from github.com/bokiko/bloxcue"*

---

## Custom Statusline

Upgrade from plain text to a visual progress bar.

| Default | Custom |
|---------|--------|
| `83.9k 41%` | `[██████░░░░░░░░░] 41%` |

**Features:**
- Visual progress bar instead of plain numbers
- Color-coded warnings (green < 60%, yellow 60-79%, red 80%+)
- Git status: branch + staged/unstaged counts
- Continuity ledger: last completed task → current focus

**Install:**
```bash
curl -o ~/.claude/scripts/status.sh \
  "https://gitlab.com/bokiko/continuous-claude-guide/-/raw/main/scripts/statusline/claude-statusline.sh"
chmod +x ~/.claude/scripts/status.sh
```

Add to `~/.claude/settings.json`:
```json
{
  "statusLine": {
    "type": "command",
    "command": "$HOME/.claude/scripts/status.sh"
  }
}
```

---

## FAQ

<details>
<summary><strong>Does this work with Cursor or VS Code extensions?</strong></summary>

No. This is designed for **Claude Code CLI** (the terminal tool). The hooks and skills system only works with the CLI.
</details>

<details>
<summary><strong>What's the difference between ledgers and handoffs?</strong></summary>

- **Ledger**: A living document that tracks your current session state, goals, and progress. Updated as you work.
- **Handoff**: A snapshot saved when you're done working. Used to resume later with full context.

Think of ledgers as "what I'm doing now" and handoffs as "what I was doing when I stopped."
</details>

<details>
<summary><strong>Do I need external services like Braintrust?</strong></summary>

No. The minimal config (`TRACE_TO_BRAINTRUST="false"`) works completely offline. Braintrust is optional for session analytics.
</details>

<details>
<summary><strong>Can I use this for multiple projects?</strong></summary>

Yes! Each project gets its own `thoughts/` directory with separate ledgers and handoffs. Initialize each project with `~/.claude/scripts/init-project.sh`.
</details>

<details>
<summary><strong>What if I forget to create a handoff?</strong></summary>

The ledger still captures your progress. It won't be as detailed as a handoff, but Claude can read the ledger to understand what you were working on.
</details>

---

## Troubleshooting

<details>
<summary><strong>"Command not found: claude"</strong></summary>

Claude Code CLI is not installed. Get it from: https://docs.anthropic.com/claude-code
</details>

<details>
<summary><strong>"Command not found: uv"</strong></summary>

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
export PATH="$HOME/.local/bin:$PATH"
# Add to ~/.bashrc or ~/.zshrc for permanence
```
</details>

<details>
<summary><strong>"No ledger found" warning</strong></summary>

Initialize your project:
```bash
cd /your/project/path
~/.claude/scripts/init-project.sh
```
</details>

<details>
<summary><strong>"Permission denied" errors</strong></summary>

macOS:
```bash
sudo chown -R $(whoami):staff /opt/claude-admin
```

Ubuntu/Fedora:
```bash
sudo chown -R $(whoami):$(whoami) /opt/claude-admin
```
</details>

<details>
<summary><strong>Hooks not executing</strong></summary>

```bash
chmod +x ~/.claude/hooks/*.sh
```
</details>

---

## File Locations

| What | Location |
|------|----------|
| Global installation | `~/.claude/` |
| Configuration | `~/.claude/.env` |
| Hooks | `~/.claude/hooks/` |
| Skills | `~/.claude/skills/` |
| Project ledgers | `your-project/thoughts/ledgers/` |
| Project handoffs | `your-project/thoughts/shared/handoffs/` |

---

## Credits

- [parcadei](https://github.com/parcadei) - Creator of [Continuous-Claude-V3](https://github.com/parcadei/Continuous-Claude-v3)

---

## License

MIT - Use it however you want.

---

<div align="center">

Made by [@bokiko](https://twitter.com/bokiko) · [bokiko.io](https://bokiko.io)

</div>
