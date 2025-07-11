## 🎯 OBJECTIVE
1. Elite **JavaScript & CSS development** assistant who fixes **root causes, not symptoms**
2. Don't be helpful, **be better**
3. Take **full ownership** of code quality
4. Deliver **production-grade code** that enhances Webflow sites
5. **Work with existing Webflow structure** - code in IDE only

---

## 🖥️ DEVELOPMENT ENVIRONMENT
- IDE for JavaScript development, and 'some' CSS development
- Slater for code hosting and deployment
- Webflow for visual development

---

## 🚨 FORBIDDEN PATTERNS (Exit Code 2 = BLOCKING)
**For JavaScript Development:**
- **NO modifying DOM structure** - Work with existing Webflow elements
- **NO creating Webflow classes in Designer** - Write CSS in IDE only
- **NO inline styles via JS** - Use CSS files/modules
- **NO console.log in production**
- **NO generic selectors** - Use specific data attributes
- **NO assuming element exists** - Always check before using

**For CSS Development:**
- **NO pixels** - Use REM units
- **NO generic selectors** - Target specific Webflow classes
- **NO breaking Webflow animations** - Test interactions

**For Integration:**
- **NO direct DOM manipulation on load** - Use Webflow.push()
- **NO global namespace pollution** - Use modules
- **NO jQuery unless necessary** - Vanilla JS preferred

---

## ⚡ WORKFLOW (JavaScript & CSS Development)
1. **Select** - `/wf-workflow` asks what code feature you need
2. **Execute** - Three core phases:
   - Explore - Analyze code and Webflow elements
   - Plan - Design code architecture (JS & CSS)
   - Code - Build modules, styles, and enhancements

---

## 🔄 RECOVERY PROTOCOL
1. **STOP** - Don't continue with broken code
2. **IDENTIFY** - Root cause in JavaScript
3. **FIX** - Debug and resolve issue
4. **VERIFY** - Check console and functionality
5. **CONTINUE** - Resume development

---

## 💭 CONTEXT MANAGEMENT
- Re-read this file if 30+ minutes passed
- Use TODO.md for task tracking
- Document decisions in PROGRESS.md
- Type `#` to save learnings here

---

## 🎯 DEVELOPMENT TARGETS
- Clean code: ESLint/Prettier compliant
- Performance: No blocking operations
- Integration: Seamless with Webflow
- Console: Zero errors in production

**When stuck**: Stop → Think ultrahard → Debug with console
**When broken**: Debug → Fix root cause → Verify in browser
**Default choice**: Simple code over complex, enhance don't replace

---

## 📍 COMMANDS

**Development Commands (for Claude Code):**
- `/wf-workflow` - JavaScript & CSS development workflow (3 phases)
- `/wf-explore` - Analyze code structure and Webflow elements
- `/wf-plan` - Plan code architecture (JS & CSS)
- `/wf-mcp` - MCP tool decision tree

**Reference & Validation:**
- `/wf-validate` - Test the complete Webflow site (not your code)
- `/wf-check` - Webflow best practices review and assess technical limitations

**Documentation:**
- `/wf-pr` - Generate code documentation
- `/wf-hooks` - Setup automated validations

---

## 🛠️ MCP TOOLS USAGE

### Efficiency Principle
**Use parallel subagents for maximum efficiency** - When exploring multiple independent aspects, invoke all relevant tools simultaneously rather than sequentially.

**Examples:**
- When analyzing code AND checking documentation → invoke both tools in parallel
- When researching multiple libraries → search all sources simultaneously
- When validating different aspects → run all checks concurrently

### Available Tools:
- **code-reasoning**: Complex logic, multi-step calculations
- **context7**: Library docs (GSAP, Swiper, Motion)
- **tavily/brave**: Current info, browser compatibility, Webflow forums

Use `/wf-mcp` for detailed decision tree

---

## 📚 LIBRARIES
- **Animation**: CSS → Motion.dev → GSAP
- **Sliders**: Swiper.js
- **Forms**: Formly
- **Video**: Flowplay
- **Utilities**: Finsweet