# /wf-validate - External Testing Framework for Webflow

**Note**: Webflow and Slater don't provide native testing capabilities. This framework describes external tools and scripts you can set up to validate your Webflow sites.

---

## ⚡ Testing Approaches
```bash
/wf-validate manual    # Manual testing checklist
/wf-validate puppeteer # Automated tests with Puppeteer
/wf-validate lighthouse # Performance testing setup
/wf-validate checklist  # Printable validation checklist
```

---

## 🎯 Manual Testing Checklist
Since Webflow lacks testing APIs, use this manual checklist:

### Essential Checks:
1. **Homepage loads** < 3s (use browser DevTools)
2. **Navigation works** all menu items  
3. **Forms submit** without errors (test each form)
4. **CMS displays** correct content
5. **No console errors** (check browser console)
6. **Mobile menu** opens/closes
7. **Images load** with proper sizing

**Tip**: Create a spreadsheet to track test results across different pages and devices.

---

## 🔍 Automated Testing Setup

### 1. 🚀 Puppeteer Setup
```js
// setup-puppeteer-tests.js
const puppeteer = require('puppeteer');

async function testWebflowSite() {
  const browser = await puppeteer.launch();
  const page = await browser.newPage();
  
  // Test homepage load
  await page.goto('https://your-site.webflow.io');
  const loadTime = await page.evaluate(() => performance.timing.loadEventEnd - performance.timing.navigationStart);
  console.log(`Page load time: ${loadTime}ms`);
  
  // Test form submission
  await page.type('[name="email"]', 'test@example.com');
  await page.click('[type="submit"]');
  
  // Check for errors
  const errors = await page.evaluate(() => {
    const errorElements = document.querySelectorAll('.w-form-error');
    return Array.from(errorElements).map(el => el.textContent);
  });
  
  await browser.close();
  return { loadTime, errors };
}
```

### 2. 📊 Lighthouse CLI
```bash
# Install
npm install -g lighthouse

# Run performance test
lighthouse https://your-site.webflow.io \
  --output html \
  --output-path ./lighthouse-report.html

# Automated CI check
lighthouse https://your-site.webflow.io \
  --output json \
  --budget-path=./budget.json
```

### 3. 📱 Cross-Browser Testing
Since Webflow doesn't provide device testing, use:
- **BrowserStack** - Paid service for real devices
- **LambdaTest** - Alternative with free tier
- **Local testing** - Use browser DevTools device emulation

### 4. 🗂️ Webflow API Limitations for Testing
**Important**: Webflow's API has significant limitations:
- **Rate limit**: 60 requests/minute
- **Read-only** for most operations
- **No testing endpoints**
- **Can't simulate user interactions**

```js
// Example: Check CMS items (within API limits)
async function checkCMSContent() {
  const response = await fetch(`https://api.webflow.com/collections/${collectionId}/items`, {
    headers: { 'Authorization': `Bearer ${token}` }
  });
  
  // Note: Can only verify data, not functionality
  const items = await response.json();
  console.log(`Found ${items.length} CMS items`);
}
```

### 5. 🔍 SEO Validation
```bash
✓ Meta titles (50-60 chars)
✓ Descriptions (150-160 chars)
✓ Open Graph tags
✓ Canonical URLs
✓ XML sitemap
✓ Schema markup
✓ Alt text coverage
```

### 6. ♿ Accessibility Audit
```js
testKeyboardNavigation();  // Tab order
testScreenReader();        // ARIA labels
testColorContrast();       // 4.5:1 minimum
testFocusIndicators();     // Visible states
```

### 7. 🔗 Link Validation
- Internal links (no 404s)
- External links (no broken)
- Anchor links (smooth scroll)
- PDF/asset links (downloadable)

### 8. 🛒 E-commerce (if applicable)
```
Cart: Add → Update → Remove
Checkout: Guest → Member
Payment: Test cards → Success/fail
Inventory: Stock updates
```

---

## 🚨 Reality Check: What's NOT Possible

❌ **Native Webflow testing** - No testing APIs or hooks
❌ **Slater integration** - No deployment testing capabilities  
❌ **Automated form testing via API** - Forms aren't accessible via API
❌ **Visual regression in platform** - Requires external tools
❌ **Performance monitoring** - Use external services like Datadog

✅ **What IS Possible**:
- External automated testing with Puppeteer/Playwright
- Manual testing with checklists
- Lighthouse performance audits
- Third-party monitoring services
- GitHub Actions for CI/CD

---

## 📊 Test Report Format
```
=== WEBFLOW VALIDATION REPORT ===
Site: example.webflow.io
Date: [timestamp]
Mode: Full

PASSED (45/50):
✅ Performance: 92/100 Lighthouse
✅ Forms: All 3 forms functional
✅ CMS: Collections loading correctly
✅ Mobile: Responsive on all devices

FAILED (5/50):
❌ Image optimization: 3 images > 500KB
❌ Alt text: Missing on 12 images
❌ Console error: undefined variable line 234
❌ Link check: 2 broken external links
❌ Contrast: Footer text 3.2:1 ratio

WARNINGS:
⚠️ CMS approaching limit (8,234/10,000 items)
⚠️ Long form labels truncated on mobile
⚠️ No 404 page configured

Action items generated: fix.md
```

---

## 🔧 Practical Testing Setup
```bash
# 1. Create testing directory
mkdir webflow-tests
cd webflow-tests
npm init -y

# 2. Install dependencies
npm install puppeteer lighthouse axios

# 3. Create test runner
touch run-tests.js

# 4. Set up CI/CD (GitHub Actions)
mkdir -p .github/workflows
touch .github/workflows/webflow-tests.yml
```

### GitHub Actions Example
```yaml
name: Webflow Site Tests

on:
  schedule:
    - cron: '0 9 * * *' # Daily at 9 AM
  workflow_dispatch:

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v2
    
    - name: Run Lighthouse
      run: |
        npm install -g lighthouse
        lighthouse https://your-site.webflow.io \
          --output json \
          --output-path ./report.json
    
    - name: Check performance
      run: |
        node check-performance.js
```

---

## 💡 Testing Best Practices

1. **Test on staging first** - Never validate on production during peak hours
2. **Use real data** - Test with actual content, not Lorem Ipsum
3. **Test edge cases** - Empty states, max content, special characters
4. **Document issues** - Screenshots + browser console logs
5. **Verify fixes** - Re-test after implementing changes

---

## 📍 Commands (Conceptual)
```bash
# These represent testing strategies, not actual CLI commands
/wf-validate manual       # Use manual checklist
/wf-validate setup        # Setup external testing
/wf-validate puppeteer    # Configure Puppeteer tests
/wf-validate lighthouse   # Run Lighthouse audits
/wf-validate api-check    # Test API endpoints (limited)
```

**Remember**: Validation requires external tools since Webflow and Slater don't provide native testing capabilities. Build your own testing pipeline!