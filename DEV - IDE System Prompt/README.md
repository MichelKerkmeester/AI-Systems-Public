# IDE System Prompt / Rules - User Guide

## 🎯 What is This?

A comprehensive set of IDE rules that transforms AI assistants into elite software engineers who:
- Fix root causes, not symptoms
- Deliver production-grade code with zero technical debt
- Optimize performance relentlessly
- Follow modern web development best practices
- **NEW:** Leverage MCP (Model Context Protocol) tools for enhanced reasoning and documentation

> [!NOTE]  
> While this system is optimized for a **Webflow + Slater** workflow, its principles can be easily adapted for any other development environment or use case.

.

## 💡 How It Works

The system enforces 10 core principles + MCP workflows:

1. **🎯 Objective** - Elite engineering, not just helpful
2. **🧠 Principles** - DRY, KISS, CSS-first approach + MCP integration
3. **🔍 Reasoning** - Explicit assumptions, evidence-based solutions
4. **🧔 MCP Tool Usage** - Code-reasoning validation, Context7 docs, web search
5. **🚦 Pre-Code Check** - Define scope before coding
6. **🛡️ Risk Management** - Document what could break
7. **🌀 Dev Planning/Execution** - Phased approach, creative solutions
8. **💬 Strategic/Tactical Comms** - Clear rationale, scannable format
9. **📚 Libraries** - Preferred tools (Motion.dev, Swiper.js, etc.)
10. **🛠️ Tech Execution** - Webflow/Slater specific rules
11. **🏎️ MCP Workflow** - Tool sequence and decision tree

.

## 🚀 Quick Setup

### For Cursor / Windsurf IDE (Recommended Setup)
1. Open your project in Cursor or Windsurf
2. Go to **Settings → Project Rules** (Cursor) or **AI Rules** (Windsurf)
3. Add each section as a separate rule for better organization:
   - Rule 1: "Objective" (Section 1)
   - Rule 2: "Principles" (Section 2)
   - Rule 3: "Reasoning" (Section 3)
   - Rule 4: "MCP Tool Usage" (Section 3A)
   - Rule 5: "Pre-Code Check" (Section 4)
   - Rule 6: "Risk Management" (Section 5)
   - Rule 7: "Dev Planning & Execution" (Sections 6A & 6B)
   - Rule 8: "Communication" (Sections 7A & 7B)
   - Rule 9: "Libraries" (Section 8)
   - Rule 10: "Tech Execution" (Sections 9A, 9B, 9C)
   - Rule 11: "MCP Workflow" (Sections 10a, 10b, 10c)
4. Enable/disable rules based on your current task

**Benefits of separate rules:**
- Toggle specific behaviors (e.g., disable "Risk Management" for quick prototypes)
- Keep context window efficient by only using needed rules
- Easier to maintain and update individual sections

**Alternative:** Create `.cursorrules` file (Cursor) or `.windsurfrules` file (Windsurf) with all rules combined

.

### For Claude Code (claude.md)
1. Create `claude.md` in your project root
2. Paste the system prompt
3. Claude Code will reference these rules automatically
4. **Important:** Ensure MCP tools are configured in your environment

.

### For Gemini CLI (gemini.md)
1. Create `gemini.md` in your project root
2. Paste the system prompt
3. Gemini will use these as context
4. **Note:** MCP integration may vary based on Gemini's tool support

.

### For Other IDEs
- **VS Code with AI extensions:** Add to `.vscode/ai-rules.md`
- **JetBrains IDEs:** Add to `.idea/ai-assistant.md`
- **Generic:** Create `AI_RULES.md` in project root

.

## 🧔 MCP Tools Overview

### Code-Reasoning (Validation Tool)
- Use AFTER internal reasoning to validate approach
- Verify complex logic and edge cases
- Explore alternative implementations

### Context7 (Library Documentation)
- Real-time library documentation
- API reference and best practices
- Compatibility verification

### Tavily/Brave Search (Current Information)
- Latest web development trends
- Browser compatibility checks
- Performance optimization techniques

.

## 📋 Usage Tips

1. **Start Simple**: Begin with core rules (1-5), add others as needed
2. **MCP Workflow**: Always think first, then validate with tools
3. **Performance First**: CSS > JS, REM units only
4. **Document Everything**: Especially non-obvious patterns
5. **Match Complexity**: Scale response detail to task size

.

## 🔗 Resources

- [Motion.dev Documentation](https://motion.dev)
- [Swiper.js](https://swiperjs.com)
- [Webflow Forums](https://forum.webflow.com)
- [Finsweet Resources](https://finsweet.com)
