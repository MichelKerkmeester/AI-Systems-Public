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
**Use**: Debug complex issues, architecture planning, step-by-step analysis
- Complex debugging sequences
- Multi-phase planning
- Alternative approach exploration
- Cause-effect chain analysis
- Revision of previous thinking

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
| Debug complex issue | | ✓ | | ✓ | | CMS re-render breaks |
| Library syntax | | | ✓ | | | GSAP ScrollTrigger |
| Forum solutions | | | | ✓ | ✓ | Collection limits |
| Architecture planning | | ✓ | | | | State management |
| Browser compatibility | | | | ✓ | | CSS Grid support |
| Performance analysis | ✓ | ✓ | ✓ | ✓ | | Complex animations |

---

## 🎯 Common Patterns

```bash
# Pattern shortcuts (use these combos)
Collection animations:  C7(gsap) + WS(forums) + CR(timing)
Debug CMS issues:      ST(analyze) + WS(known bugs) + C7(reinit)
Form validation:       CR(logic) + WS(submission api) + ST(error flow)
Performance fix:       CR(render cycles) + C7(optimize) + WS(tips) + ST(bottlenecks)
API integration:       ST(data flow) + WS(rate limits) + CR(throttling)
Responsive system:     CR(calculations) + WS(best practices)
Complex debugging:     ST(step-by-step) + WS(similar issues) + CR(analysis)
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
- **CR fails** → Break problem into smaller parts
- **WS fails** → Try TV/BR → Specific documentation sites
- **ST fails** → Manual structured analysis
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