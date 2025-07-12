# Claude Code - Instructions + Commands - User Guide

Transform your development workflow with intelligent commands and automated validation for Webflow projects.

> [!NOTE]  
> While this system is optimized for a **Webflow + Slater** workflow, its principles and commands can be easily adapted for any other development environment or use case.

.

## 🚀 Quick Install via Claude Code Chat

The easiest way to install is through Claude Code itself. Simply paste this request:
```
Please install the Claude Code System from:
https://github.com/MichelKerkmeester/AI-Systems-Public/tree/main/DEV%20-%20Claude%20Code%20-%20Instructions%20%2B%20Commands
```

Claude will automatically:
- ✅ Backup existing configuration
- ✅ Install CLAUDE.md with Webflow-focused instructions  
- ✅ Create .claude directory structure
- ✅ Install all command modules
- ✅ Configure project settings
- ✅ Set up documentation templates

**Installation time: ~2 minutes**

.

## 📋 What You Get

### Powerful Commands
| Command | Options | Purpose |
|---------|---------|---------|
| **`/workflow`** | `explore` \| `plan` \| `code` | Structured development phases |
| **`/check`** | `quick` \| `full` \| `fix` | Code validation & auto-fixes |
| **`/validate`** | `manual` \| `puppeteer` \| `lighthouse` | Testing frameworks |
| **`/mcp`** | - | MCP tool decision tree |
| **`/pr`** | - | Documentation best practices |

### Project Structure
```
your-project/
├── CLAUDE.md              # System instructions
├── .claude/
│   ├── docs/              # Active documentation
│   │   ├── PLANNING.md    # Project strategy
│   │   └── TASK.md        # Task tracking
│   ├── commands/          # Command definitions
│   │   ├── workflow.md
│   │   ├── check.md
│   │   ├── validate.md
│   │   ├── mcp.md
│   │   └── pr.md
│   ├── templates/         # Reference formats
│   └── settings.json      # Configuration
```
.

## 💡 Basic Usage

### Start Your Development Workflow
```bash
# Analyze existing Webflow structure
/workflow explore

# Plan your enhancement architecture  
/workflow plan

# Get implementation guidance
/workflow code
```

### Validate Your Code
```bash
# Quick 5-minute check before commits
/check quick

# Comprehensive audit before deployment
/check full

# Auto-fix found issues
/check fix
```

### Test Your Implementation
```bash
# Manual testing checklist
/validate manual

# Set up automated tests
/validate puppeteer
```

.

## ⚙️ Customization

### Project Context
Edit `.claude/docs/PLANNING.md` to define:
- Project goals and constraints
- Technical architecture
- Team conventions

### Task Management
Update `.claude/docs/TASK.md` to track:
- Current work in progress
- Completed tasks
- Next priorities

### Custom Commands
Add new commands to `.claude/commands/`:
```markdown
# your-command.md
Execute these steps for $ARGUMENTS:
1. Your custom logic
2. Project-specific tasks
```

.

## 🛠️ Manual Installation

If you prefer manual setup:

1. **Prerequisites**: Node.js 20+, npm 8+
2. **Download**: Clone the GitHub repository
3. **Copy**: Move files to your project
4. **Configure**: Adjust CLAUDE.md for your needs

.

## 📚 Learn More

- **Detailed Documentation**: Check individual command files
- **Advanced Configuration**: See `.claude/templates/`
- **Troubleshooting**: Ask Claude directly
- **Updates**: Watch the [GitHub repository](https://github.com/MichelKerkmeester/AI-Systems-Public)

---

*Built for developers who value intelligent automation and clean code.*
