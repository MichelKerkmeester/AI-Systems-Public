# /check - Webflow Best Practices & Technical Limitations

## ⚡ Check Modes
```bash
/check quick    # 5-min essentials
/check full     # 15-min comprehensive
/check [area]   # Specific (performance/seo/a11y)
/check fix      # Generate fixes
```

## 🚨 Forbidden Patterns (Auto-scan)
```js
Promise.all([
  scanForPixels(),           // Must use REM
  scanForGenericSelectors(), // Need data-*
  scanForConsoleLog(),       // No production logs
  scanForDOMModification(),  // No structure changes
  scanForjQuery(),           // Prefer vanilla
  scanForGlobalPollution(),  // Use modules
  scanForBlockingAnimations() // Check HW accel
]);
```

**Exit Code 2**: DOM mods, pixels, generic selectors, no Webflow.push(), console.log, DOMContentLoaded, non-HW accel transforms

## 📋 Quick Check (5 min)
```
PARALLEL: CR(perf) + WS(updates) + CR(architecture) + C7(libs)
→ Forbidden patterns → Performance → Errors → Mobile
```

## 🔍 Full Audit

### 1. Performance
```js
Promise.all([
  CR('analyze animation performance'),
  C7('motion.dev optimization patterns'),
  WS('Webflow performance 2025')
]);
```
- CSS transitions first
- Motion.dev mini (2.6kb) for most cases
- Motion.dev full (5.2kb) if scroll/spring needed
- GSAP only for complex timelines/morphing
- 60 FPS target + hardware acceleration

### 2. SEO
- Meta 150-160 chars
- OG tags, schema markup
- URL structure, sitemap
- 500 static pages max

### 3. A11Y
- ARIA labels, keyboard nav
- 4.5:1 contrast minimum
- Reduced motion support
- Known Webflow limitations (focus styles, dynamic content)

### 4. CMS
- 10K items per collection
- 30 fields max (25 recommended)
- Reference/multi-ref performance
- Query optimization strategies

### 5. Mobile
- Touch targets 44x44px
- Viewport meta correct
- iOS scroll issues fixed
- Android Chrome tested

## 🔧 Fix Generation
```js
// When issues found, generate:
1. Immediate fixes (< 5 min)
2. Refactor suggestions (if needed)
3. Webflow-specific workarounds
4. Performance impact estimates
```

## 📊 Report Format
```
✅ PASSED (3)
- Hardware acceleration used
- REM units throughout
- Data attributes present

⚠️ WARNINGS (2)
- Collection list could virtualize at 50+ items
- Consider Motion.dev for smoother transitions

❌ FAILURES (1)
- console.log found in production [line 47]
  FIX: Remove or wrap in if(DEBUG) check
```