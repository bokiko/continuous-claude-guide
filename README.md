<div align="center">

# Continuous-Claude

<h3>Give Claude Code a memory. Pick up where you left off, every time.</h3>

<p>
  <a href="#quick-start---macos">
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

## Quick Start - macOS

Copy and paste these commands:

### Install Prerequisites

```bash
# Install Homebrew if not installed
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# Install required packages
brew install node python@3.12 git jq
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

---

## Quick Start - Ubuntu

```bash
# Install prerequisites
sudo apt update
sudo apt install -y git curl sqlite3 jq python3 python3-venv python3-pip
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
sudo apt-get install -y nodejs

# Clone and install
mkdir -p ~/projects && cd ~/projects
git clone https://github.com/parcadei/Continuous-Claude.git
cd Continuous-Claude
curl -LsSf https://astral.sh/uv/install.sh | sh
source ~/.bashrc
./install-global.sh
echo 'TRACE_TO_BRAINTRUST="false"' > ~/.claude/.env

# Set up workspace
sudo mkdir -p /opt/claude-admin
sudo chown $(whoami):$(whoami) /opt/claude-admin
cd /opt/claude-admin
~/.claude/scripts/init-project.sh
echo 'alias sysadmin="cd /opt/claude-admin && claude"' >> ~/.bashrc
source ~/.bashrc
```

---

## Quick Start - Fedora

```bash
# Install prerequisites
sudo dnf install -y git curl sqlite jq python3 python3-pip nodejs

# Clone and install
mkdir -p ~/projects && cd ~/projects
git clone https://github.com/parcadei/Continuous-Claude.git
cd Continuous-Claude
curl -LsSf https://astral.sh/uv/install.sh | sh
source ~/.bashrc
./install-global.sh
echo 'TRACE_TO_BRAINTRUST="false"' > ~/.claude/.env

# Set up workspace
sudo mkdir -p /opt/claude-admin
sudo chown $(whoami):$(whoami) /opt/claude-admin
cd /opt/claude-admin
~/.claude/scripts/init-project.sh
echo 'alias sysadmin="cd /opt/claude-admin && claude"' >> ~/.bashrc
source ~/.bashrc
```

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

### bloxcue - Reduce Token Usage by 90%

Once you have Continuous-Claude set up, add [**bloxcue**](https://github.com/bokiko/bloxcue) to dramatically reduce your token usage.

| Problem | Solution |
|---------|----------|
| Large CLAUDE.md files load on every prompt | bloxcue loads only relevant context blocks |
| ~8,500 tokens wasted per prompt | ~800 tokens loaded (only what's needed) |
| Hit token limits faster | Save ~7,000+ tokens per prompt |

**Quick Install:**
```bash
git clone https://github.com/bokiko/bloxcue.git
cd bloxcue
./install.sh
```

Or just tell Claude: *"Install bloxcue for me from github.com/bokiko/bloxcue"*

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

- [Anand Chowdhary](https://github.com/AnandChowdhary) - Creator of [Continuous-Claude](https://github.com/AnandChowdhary/continuous-claude)

---

## License

MIT - Use it however you want.

---

<div align="center">

Made by [@bokiko](https://twitter.com/bokiko) · [bokiko.io](https://bokiko.io)

</div>
