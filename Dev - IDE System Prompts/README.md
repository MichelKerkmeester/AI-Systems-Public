# IDE System Prompt / Rules - Setup Guide

## 🎯 What is This?

A comprehensive set of IDE rules that transforms AI assistants into elite software engineers who:
- Fix root causes, not symptoms
- Deliver production-grade code with zero technical debt
- Optimize performance relentlessly
- Follow modern web development best practices

**Perfect for:** Webflow developers, frontend engineers, and anyone building performant web applications.

.

## 💡 How It Works

The system enforces 10 core principles:

1. **🎯 Objective** - Elite engineering, not just helpful
2. **🧠 Principles** - DRY, KISS, CSS-first approach
3. **🔍 Reasoning** - Explicit assumptions, evidence-based solutions
4. **🚦 Pre-Code Check** - Define scope before coding
5. **🛡️ Risk Management** - Document what could break
6. **🌀 Dev Planning/Execution** - Phased approach, creative solutions
7. **💬 Strategic/Tactical Comms** - Clear rationale, scannable format
8. **📚 Libraries** - Preferred tools (Motion.dev, Swiper.js, etc.)
9. **🛠️ Tech Execution** - Webflow/Slater specific rules

.

## 🚀 Quick Setup

### For Cursor IDE (Recommended Setup)
1. Open your project in Cursor
2. Go to **Settings → Project Rules**
3. Add each section as a separate rule for better organization:
   - Rule 1: "Objective" (Section 1)
   - Rule 2: "Principles" (Section 2)
   - Rule 3: "Reasoning" (Section 3)
   - Rule 4: "Pre-Code Check" (Section 4)
   - Rule 5: "Risk Management" (Section 5)
   - Rule 6: "Dev Planning & Execution" (Sections 6A & 6B)
   - Rule 7: "Communication" (Sections 7A & 7B)
   - Rule 8: "Libraries" (Section 8)
   - Rule 9: "Tech Execution" (Sections 9A, 9B, 9C)
   - Rule 10: "Test & Validate" (Section 10)
4. Enable/disable rules based on your current task

**Benefits of separate rules:**
- Toggle specific behaviors (e.g., disable "Risk Management" for quick prototypes)
- Keep context window efficient by only using needed rules
- Easier to maintain and update individual sections

**Alternative:** Create `.cursorrules` file with all rules combined

.

### For Claude Code (Claude.md)
1. Create `claude.md` in your project root
2. Paste the system prompt
3. Claude Code will reference these rules automatically

.

### For Gemini CLI (gemini.md)
1. Create `gemini.md` in your project root
2. Paste the system prompt
3. Gemini will use these as context

.

### For Other IDEs
- **VS Code with AI extensions:** Add to `.vscode/ai-rules.md`
- **JetBrains IDEs:** Add to `.idea/ai-assistant.md`
- **Generic:** Create `AI_RULES.md` in project root