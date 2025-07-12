# /check - Webflow Best Practices & Technical Limitations

---

## ⚡ Check Modes
```bash
/check quick    # 5-min essentials
/check full     # 15-min comprehensive
/check [area]   # Specific (performance/seo/a11y)
/check fix      # Generate fixes
```

---

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

---

## 📋 Quick Check (5 min)
```
PARALLEL: CR(perf) + WS(updates) + CR(architecture) + C7(libs)
→ Forbidden patterns → Performance → Errors → Mobile
```

---

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
- Known: Slider/form/filter issues

### 4. Code Quality
- Module patterns
- Event delegation
- Debounce/throttle
- Memory leaks
- Async handling

### 5. Slater
- No DOMContentLoaded
- Export structure
- Version control
- Build optimization

### 6. Browser Support
- Last 2 versions major browsers
- iOS 12+, Android 8+

### 7. Mobile
- 44x44px touch targets
- Viewport meta
- No horizontal scroll

### 8. Animation
```js
// ✅ HW accelerated
animate(".box", { transform: "translateX(100px)" })
// ❌ Not accelerated  
animate(".box", { x: 100 })

// ✅ Use filter
animate(el, { filter: "drop-shadow(10px 10px)" })
// ❌ Avoid boxShadow
```

---

## 🎯 Platform Limits (July 2025)

**CMS**: 10k items, 30 fields, 5 refs, 25 multi-refs, draft mode, individual publish
**API**: 60 req/min, 10k items, beta under /beta
**Hosting**: 100GB/mo, 25GB storage, no SSR, per-page JS
**New**: AI Assistant, Variable Modes, GSAP owned

**JS Constraints**: No Node, browser only, use Webflow.push(), re-attach after CMS render
**CSS Limits**: No vars in Designer, limited pseudo, custom via embed

---

## 📊 Report Format
```
Health Score: 85/100

🚨 Critical (3)
- Pixels in /styles/custom.css
- Generic .container selector
- console.log at line 42

⚠️ Warnings (5)
- 8,500 CMS items
- Missing alt text
- Small touch targets

✅ Passed (15)
- Performance targets met
- SEO configured
```

---

## 🔧 Quick Fixes
```bash
Issues → Solutions:
CMS slow → Pagination + draft mode
Janky → Motion.dev transform strings
Forms → Check Webflow.push()
Mobile → 44px targets + Motion mini
SEO → Meta + AI Assistant

Workarounds:
No CSS vars → Variable Modes
Collections → Virtual scroll + individual publish
No websockets → Poll + API
State → localStorage + URL params
Animations → Motion.dev mini default
```

---

## 📍 Commands
```bash
/check              # Menu
/check quick        # Essentials
/check full         # Complete
/check [area]       # Specific
/check report       # Generate
/check fix [issue]  # Auto-fix
/check limits       # Reference
```

**Run before deployment. Use parallel MCP for validation.**