# /mcp - MCP Tool Decision Tree

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

## 🛑 Skip Tools When
- Simple CSS transitions (< 5s to code)
- Basic event handlers (onClick, onChange)
- Known syntax (don't look up what you know)
- Native Webflow interactions suffice
- Standard DOM operations

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
- **BR**: Privacy-focused search
- Webflow University articles
- Forum solutions & workarounds
- Browser compatibility (caniuse)
- Performance benchmarks
- Recent updates & deprecations

## 📊 Decision Matrix

```js
const toolDecision = {
  // Animation task
  animation: {
    simple: null, // No tools, use CSS
    medium: ['C7'], // Motion.dev docs
    complex: ['CR', 'C7', 'WS'] // Math + Docs + Examples
  },
  
  // Webflow-specific
  webflow: {
    limits: ['WS'], // Forums have answers
    workaround: ['WS', 'CR'], // Find + Implement
    integration: ['WS', 'C7', 'CR'] // Full solution
  },
  
  // Performance
  performance: {
    measure: ['CR'], // Calculate metrics
    optimize: ['CR', 'WS'], // Analyze + Best practices
    debug: ['CR', 'ST', 'WS'] // Full investigation
  }
};
```

## 🚀 Common Patterns

### Pattern 1: Library Implementation
```js
Promise.all([
  C7({library: 'swiper', topic: 'responsive config'}),
  WS({query: 'swiper webflow integration 2025'}),
  CR({task: 'calculate optimal slide dimensions'})
]);
```

### Pattern 2: Debugging Complex Issue
```js
Promise.all([
  CR({task: 'analyze performance bottleneck', data: metrics}),
  WS({query: 'webflow collection list performance'}),
  ST({task: 'alternative architecture approaches'})
]);
```

### Pattern 3: Feature Planning
```js
Promise.all([
  ST({task: 'design user flow', constraints: webflowLimits}),
  WS({query: 'similar implementations examples'}),
  C7({library: 'relevant-lib', topic: 'capabilities'})
]);
```

## ⏱️ Time Guidelines
- **0-5s**: No tools needed
- **5-30s**: 1-2 tools max
- **30s+**: Full parallel suite
- **Stuck 10min+**: Use recovery protocol

## 🎯 Remember
1. **Think first** - Tools enhance, not replace reasoning
2. **Batch queries** - One parallel call > Multiple sequential
3. **Be specific** - Vague queries = Vague results
4. **Check cache** - Recent queries might be cached
5. **Fail fast** - If tools don't help in 2 attempts, try manual