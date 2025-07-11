# /wf-validate - Webflow-Specific Quality Validation

When you type `/wf-validate`, I'll ask:

## 🎯 Validation Level
```
"What validation do you need?

1. **Quick Check** (~2 min) - Console errors, basic checks
2. **Performance** (~5 min) - PageSpeed Insights, Core Web Vitals
3. **Full Audit** (~15 min) - Performance + Accessibility + SEO
4. **Forms** - Test form validation and submissions
5. **Specific Page** - Test single page/component

Note: Always test on PUBLISHED site in incognito mode!"
```

## ⚡ Quick Check (Level 1)

### Webflow Designer Checks
```
✓ No inline styles (use classes only)
✓ Semantic class names (not "Div Block 47")
✓ Proper heading hierarchy (H1→H2→H3)
✓ All images have alt text
✓ Forms have proper labels
✓ No broken CMS references
```

### Console Validation (Run on published site)
```javascript
// Clear console first
console.clear();

// Check for errors
const errors = console.error ? '❌ Console has errors!' : '✅ No console errors';
console.log(errors);

// Webflow-specific checks
const checks = {
  jQuery: typeof $ !== 'undefined' ? '✅' : '❌',
  Webflow: typeof Webflow !== 'undefined' ? '✅' : '❌',
  SlaterScripts: document.querySelectorAll('[data-slater]').length,
  Forms: document.querySelectorAll('form').length,
  CMSItems: document.querySelectorAll('.w-dyn-item').length,
  LazyImages: document.querySelectorAll('img[loading="lazy"]').length
};

console.table(checks);

// Quick performance
console.log(`Load time: ${performance.timing.loadEventEnd - performance.timing.navigationStart}ms`);
```

## 🚀 Performance Testing (Level 2)

### PageSpeed Insights (Recommended)
```
1. Go to: https://pagespeed.web.dev/
2. Enter your published Webflow URL
3. Run test (will test mobile + desktop)
4. Target scores:
   - Performance: 90+
   - Accessibility: 100
   - Best Practices: 90+
   - SEO: 90+
```

### Key Metrics to Watch
```
Core Web Vitals (Mobile):
- LCP < 2.5s (Largest Contentful Paint)
- FID < 100ms (First Input Delay)  
- CLS < 0.1 (Cumulative Layout Shift)

Webflow-Specific:
- Images optimized (WebP format)
- Fonts loaded efficiently
- No render-blocking scripts
- Interactions don't impact CLS
```

### Performance Tips
```
⚠️ Run test 5-10 times and average results
⚠️ Test in incognito to avoid extensions
⚠️ Test both staging and custom domain
⚠️ Mobile scores matter more than desktop
```

## 🔍 Full Audit (Level 3)

### 1. Lighthouse via Chrome DevTools
```
1. Open site in Chrome Incognito
2. Right-click → Inspect → Lighthouse tab
3. Configure:
   - Device: Mobile
   - Categories: All
   - Throttling: Simulated
4. Generate report
```

### 2. Accessibility Testing
```
Browser Extensions:
- WAVE (WebAIM) - Best for Webflow
- axe DevTools
- Lighthouse (built-in)

Check for:
✓ Color contrast (4.5:1 minimum)
✓ Keyboard navigation works
✓ Focus indicators visible
✓ ARIA labels on icons
✓ Form labels connected
```

### 3. SEO Validation
```
Webflow SEO Checklist:
□ All pages have unique titles
□ Meta descriptions filled
□ Open Graph configured
□ Sitemap generated
□ 301 redirects set up
□ Canonical URLs correct
□ Schema markup (if needed)
```

## 📝 Form Validation (Level 4)

### Test Form Functionality
```javascript
// Test all forms on page
document.querySelectorAll('form').forEach((form, index) => {
  console.log(`Form ${index + 1}:`, {
    action: form.action || 'Webflow default',
    method: form.method,
    fields: form.querySelectorAll('input, textarea, select').length,
    required: form.querySelectorAll('[required]').length,
    hasHoneypot: form.querySelector('[name="field"]') ? 'Yes' : 'No'
  });
});
```

### Webflow Form Testing
```
1. Submit with all fields empty
   - Should show validation messages
2. Submit with invalid email
   - Should catch format errors
3. Submit with valid data
   - Should show success message
   - Check Webflow dashboard for submission
4. Test on mobile
   - Keyboard should be appropriate
   - Fields should be accessible
```

### Custom Validation (Slater)
```javascript
// Example: ZIP code validation
const zipField = document.querySelector('input[name="zip"]');
if (zipField) {
  zipField.addEventListener('blur', function() {
    const zipRegex = /^\d{5}(-\d{4})?$/;
    if (!zipRegex.test(this.value)) {
      this.setCustomValidity('Please enter valid ZIP');
    } else {
      this.setCustomValidity('');
    }
  });
}
```

## 🛠️ Webflow-Specific Checks

### Publishing & Hosting
```
□ Custom domain connected
□ SSL certificate active
□ WWW redirect configured
□ 404 page designed
□ Favicon uploaded
□ Webclip uploaded
```

### Performance Optimizations
```
□ Images < 500KB (ideally < 200KB)
□ Videos hosted externally
□ Fonts limited to 2-3 families
□ Animations use transform/opacity
□ Lazy loading enabled
□ Minification enabled
```

### CMS & Dynamic Content
```
□ CMS limits checked (10k items)
□ Collection lists optimized
□ Pagination implemented
□ Filters work correctly
□ Empty states designed
```

## 📊 Reporting Results

### Quick Report Format
```
✅ Performance: 92/100 (Mobile)
✅ Accessibility: 100/100
⚠️ Best Practices: 87/100 (HTTP images found)
✅ SEO: 98/100

Issues to fix:
1. Optimize hero image (currently 1.2MB)
2. Add alt text to gallery images
3. Enable lazy loading on blog posts
```

### Detailed Report for Client
```markdown
## Webflow Site Validation Report
Date: [Today]
URL: [site].webflow.io

### Performance Metrics
- PageSpeed Score: 92 (Excellent)
- Load Time: 2.1s
- Time to Interactive: 2.8s

### Accessibility
- WAVE: 0 errors, 2 alerts
- Keyboard Nav: Fully functional
- Screen Reader: Tested with NVDA

### Recommendations
1. Immediate: [Critical fixes]
2. Next Sprint: [Improvements]
3. Future: [Nice-to-haves]
```

## 🚨 Common Webflow Issues

### Performance Killers
- Huge hero images (use WebP, <500KB)
- Too many fonts (stick to 2-3)
- Complex Lottie animations
- Embedded videos (use facade)
- Too many Collection Lists

### Quick Fixes
```
Image too large → Webflow's built-in optimizer
Slow interactions → Use transform, not position
CLS issues → Set explicit dimensions
Font flash → Use font-display: swap
Forms broken → Check Webflow project settings
```

## Next Steps
- **All Pass**: Publish to production
- **Issues Found**: Prioritize by impact
- **Need Help**: "Should I optimize images or fix CLS first?"
- **A/B Testing**: Consider Optibase for testing changes