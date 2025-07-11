# /wf-mcp - MCP Tool Decision Tree

---

## ⚡ Core Principle: PARALLEL EXECUTION
**Always run independent queries simultaneously!** Tool overhead: ~1-3s each

```js
// ❌ SLOW - Sequential (avoid)
await invoke('context7', {library: 'gsap'});
await invoke('web_search', {query: 'webflow forums'});

// ✅ FAST - Parallel (preferred)
Promise.all([
  invoke('context7', {library: 'gsap', topic: 'timeline'}),
  invoke('web_search', {query: 'webflow collection list'}),
  invoke('code-reasoning', {task: 'calculate responsive sizes'})
]);
```

**Performance math**: 3 tools × 2s = 6s sequential vs 2s parallel

---

## 🛑 Skip Tools When
- Simple CSS transitions (< 5s to code)
- Basic event handlers (onClick, onChange)
- Known syntax (don't look up what you know)
- Native Webflow interactions suffice
- Standard DOM operations

---

## 🔧 Tool Reference

### **CR** (code-reasoning)
**Use**: Complex math, algorithms, performance calculations
- Responsive breakpoint calculations
- Collection list pagination logic
- Animation timing & sequencing
- State machine design
- Performance optimization math

### **ST** (sequential-thinking)
**Use**: General planning, strategy design, non-code problem solving
- Multi-phase project planning
- Strategy development
- Alternative approach exploration
- Process design & workflow
- Decision tree creation

### **C7** (context7)
**Use**: Library documentation (GSAP, Swiper, Motion, Three.js, Lottie)
- Exact API syntax
- Method signatures
- Configuration options
- Library best practices
- Version-specific features

### **WS/TV/BR** (web_search/tavily/brave)
**Use**: Current info, forums, compatibility, Webflow-specific
- **WS**: General web search, broad topics
- **TV**: Specialized search, advanced options
- **BR**: Privacy-focused, alternative results
- **Targets**: Webflow Forums, MDN, CanIUse, Stack Overflow

### **WF** (web_fetch)
**Use**: Retrieve specific URLs and full content
- Complete documentation pages
- Full forum thread content
- Specific code examples
- API documentation
- Tutorial content

### **WF-API** (Webflow MCP Server - when available)
**Use**: Direct Webflow API integration
- CMS CRUD operations
- Site configuration management
- Content synchronization
- Publishing automation
- Form submission handling

---

## 📊 Decision Matrix

| Task | CR | ST | C7 | WS | WF | Example |
|------|:--:|:--:|:--:|:--:|:--:|---------|
| Math/calculations | ✓ | | | | | Grid spacing, responsive values |
| Debug code issue | ✓ | | | ✓ | | CMS re-render breaks |
| Library syntax | | | ✓ | | | GSAP ScrollTrigger |
| Forum solutions | | | | ✓ | ✓ | Collection limits |
| Project planning | | ✓ | | | | Implementation strategy |
| Browser compatibility | | | | ✓ | | CSS Grid support |
| Code performance | ✓ | | ✓ | ✓ | | Animation optimization |

---

## 🎯 Common Patterns

```bash
# Pattern shortcuts (use these combos)
Collection animations:  C7(motion.dev) + WS(webflow) + CR(performance)
Debug CMS issues:      CR(analyze code) + WS(2025 API changes) + C7(reinit)
Form validation:       CR(validation logic) + WS(submission api) + ST(ux flow)
Performance fix:       CR(code analysis) + C7(motion.dev mini) + WS(tips)
API integration:       ST(plan flow) + WS(new draft mode) + CR(implementation)
Responsive system:     CR(calculations) + WS(best practices)
Code debugging:        CR(analyze problem) + WS(similar issues) + C7(syntax)
Animation choice:      C7(motion.dev vs gsap) + CR(bundle size) + WS(use cases)
```

---

## 🚨 Failure Recovery

```js
// Primary attempt with fallback chain
try {
  await invoke('context7', {library: 'gsap'});
} catch (error) {
  console.warn('C7 failed, trying fallback...');
  try {
    await invoke('web_search', {query: 'GSAP documentation'});
  } catch {
    // Use cached knowledge or manual approach
    applyKnownPattern();
  }
}
```

**Fallback chains**:
- **C7 fails** → WS official docs → Manual search
- **CR fails** → Break code problem into smaller parts
- **WS fails** → Try TV/BR → Specific documentation sites
- **ST fails** → Manual planning/strategy session
- **WF fails** → Try different URL → WS for cached version

---

## 📍 Commands

```bash
/wf-mcp              # Full decision tree
/wf-mcp quick        # Rapid tool selector
/wf-mcp [tool]       # Specific tool guide (e.g., /wf-mcp CR)
/wf-mcp diagnose     # Map current error → best tool
/wf-mcp benchmark    # Tool performance stats
/wf-mcp fallback     # Manual alternatives when tools fail
/wf-mcp parallel     # Parallel execution examples

# Quick queries
/wf-mcp animation    # Best tools for animation tasks
/wf-mcp debug        # Debugging tool combinations
/wf-mcp performance  # Performance analysis tools
```

---

## 💡 Pro Tips

1. **Parallel first**: Multiple aspects = multiple tools simultaneously
2. **Know overhead**: Each tool ~1-3s, batch wisely
3. **Cache results**: Reuse responses in same session
4. **Webflow context**: Always include "Webflow" in searches
5. **Tool synergy**: CR+C7 for math-heavy animations, ST+WS for debugging

**Remember**: Speed comes from parallel execution, not from guessing which tool to use!