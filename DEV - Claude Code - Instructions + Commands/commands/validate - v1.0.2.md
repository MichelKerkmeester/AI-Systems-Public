# /validate - External Testing Framework for Webflow

**Note**: Webflow and Slater don't provide native testing capabilities. This framework describes external tools and scripts you can set up to validate your Webflow sites.

## ⚡ Testing Approaches
```bash
/validate manual    # Manual testing checklist
/validate puppeteer # Automated tests with Puppeteer
/validate lighthouse # Performance testing setup
/validate checklist  # Printable validation checklist
```

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

## 🤖 Automated Testing with Puppeteer

### Setup
```bash
npm install --save-dev puppeteer
mkdir tests
```

### Basic Test Script
```js
// tests/basic-checks.js
const puppeteer = require('puppeteer');

async function runTests() {
  const browser = await puppeteer.launch();
  const page = await browser.newPage();
  
  // Test 1: Homepage loads
  await page.goto('https://your-site.webflow.io');
  const title = await page.title();
  console.log('✓ Homepage loaded:', title);
  
  // Test 2: Check for console errors
  page.on('console', msg => {
    if (msg.type() === 'error') {
      console.log('✗ Console error:', msg.text());
    }
  });
  
  // Test 3: Navigation works
  const navLinks = await page.$$('[data-nav-link]');
  console.log('✓ Found nav links:', navLinks.length);
  
  // Test 4: Forms exist
  const forms = await page.$$('form');
  console.log('✓ Found forms:', forms.length);
  
  // Test 5: Images loaded
  const images = await page.$$eval('img', imgs => 
    imgs.map(img => ({
      src: img.src,
      loaded: img.complete
    }))
  );
  const failedImages = images.filter(img => !img.loaded);
  if (failedImages.length > 0) {
    console.log('✗ Failed images:', failedImages);
  }
  
  await browser.close();
}

runTests();
```

### Advanced Webflow Tests
```js
// tests/webflow-specific.js

async function testWebflowFeatures() {
  const browser = await puppeteer.launch();
  const page = await browser.newPage();
  
  // Test Collection Lists
  await page.goto('https://your-site.webflow.io/products');
  const items = await page.$$('.w-dyn-item');
  console.log('✓ Collection items:', items.length);
  
  // Test Interactions (wait for animations)
  await page.waitForTimeout(2000);
  const animatedElements = await page.$$('[data-animate]');
  console.log('✓ Animated elements:', animatedElements.length);
  
  // Test Form Submission
  await page.goto('https://your-site.webflow.io/contact');
  await page.type('[name="email"]', 'test@example.com');
  await page.type('[name="name"]', 'Test User');
  // Note: Don't actually submit in tests
  
  await browser.close();
}
```

## 🚀 Performance Testing with Lighthouse

### Setup
```bash
npm install --save-dev lighthouse
```

### Lighthouse Script
```js
// tests/performance.js
const lighthouse = require('lighthouse');
const chromeLauncher = require('chrome-launcher');

async function runLighthouse(url) {
  const chrome = await chromeLauncher.launch({chromeFlags: ['--headless']});
  const options = {
    logLevel: 'info',
    output: 'json',
    onlyCategories: ['performance'],
    port: chrome.port
  };
  
  const runnerResult = await lighthouse(url, options);
  
  // Parse results
  const reportJson = runnerResult.report;
  const report = JSON.parse(reportJson);
  
  console.log('Performance Score:', report.categories.performance.score * 100);
  console.log('Metrics:');
  console.log('- First Contentful Paint:', report.audits['first-contentful-paint'].displayValue);
  console.log('- Speed Index:', report.audits['speed-index'].displayValue);
  console.log('- Total Blocking Time:', report.audits['total-blocking-time'].displayValue);
  
  await chrome.kill();
}

runLighthouse('https://your-site.webflow.io');
```

## 📋 Visual Regression Testing

### Setup Percy (Optional)
```bash
npm install --save-dev @percy/puppeteer
```

### Percy Integration
```js
const { percySnapshot } = require('@percy/puppeteer');

async function visualTests() {
  const browser = await puppeteer.launch();
  const page = await browser.newPage();
  
  await page.goto('https://your-site.webflow.io');
  await percySnapshot(page, 'Homepage');
  
  await page.goto('https://your-site.webflow.io/about');
  await percySnapshot(page, 'About Page');
  
  await browser.close();
}
```

## 🔄 Continuous Integration

### GitHub Actions Example
```yaml
# .github/workflows/test.yml
name: Webflow Site Tests

on:
  schedule:
    - cron: '0 8 * * *' # Daily at 8 AM
  workflow_dispatch:

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - uses: actions/setup-node@v2
      - run: npm install
      - run: npm test
      - name: Upload results
        uses: actions/upload-artifact@v2
        with:
          name: test-results
          path: test-results/
```

## 📊 Test Reporting

### Simple HTML Report
```js
// tests/generate-report.js
const fs = require('fs');

function generateReport(results) {
  const html = `
    <!DOCTYPE html>
    <html>
    <head>
      <title>Webflow Test Results</title>
      <style>
        body { font-family: Arial, sans-serif; margin: 40px; }
        .pass { color: green; }
        .fail { color: red; }
        table { border-collapse: collapse; width: 100%; }
        th, td { border: 1px solid #ddd; padding: 8px; text-align: left; }
      </style>
    </head>
    <body>
      <h1>Webflow Site Test Results</h1>
      <p>Generated: ${new Date().toLocaleString()}</p>
      <table>
        <tr>
          <th>Test</th>
          <th>Status</th>
          <th>Details</th>
        </tr>
        ${results.map(test => `
          <tr>
            <td>${test.name}</td>
            <td class="${test.passed ? 'pass' : 'fail'}">
              ${test.passed ? '✓ PASS' : '✗ FAIL'}
            </td>
            <td>${test.details}</td>
          </tr>
        `).join('')}
      </table>
    </body>
    </html>
  `;
  
  fs.writeFileSync('test-report.html', html);
}
```

## 🎯 Webflow-Specific Validations

### 1. CMS Limits Check
```js
async function checkCMSLimits() {
  // Check collection item count
  const items = await page.$$('.w-dyn-item');
  if (items.length > 9000) {
    console.warn('⚠️ Approaching 10k CMS limit');
  }
}
```

### 2. Form Validation
```js
async function validateForms() {
  const forms = await page.$$('form');
  for (const form of forms) {
    const action = await form.evaluate(el => el.action);
    if (!action.includes('webflow.com')) {
      console.warn('⚠️ Form may not be connected to Webflow');
    }
  }
}
```

### 3. Asset Performance
```js
async function checkAssets() {
  const images = await page.$$eval('img', imgs => 
    imgs.map(img => ({
      src: img.src,
      size: img.naturalWidth * img.naturalHeight
    }))
  );
  
  const largeImages = images.filter(img => img.size > 1000000);
  if (largeImages.length > 0) {
    console.warn('⚠️ Large images detected:', largeImages);
  }
}
```

## 📝 Manual Testing Template

```markdown
## Webflow Site Testing Checklist

**Site URL**: ___________________
**Date**: ___________________
**Tester**: ___________________

### Desktop Testing
- [ ] Homepage loads < 3s
- [ ] All navigation links work
- [ ] Forms submit successfully
- [ ] CMS content displays
- [ ] Animations run smoothly
- [ ] No console errors
- [ ] SEO meta tags present

### Mobile Testing (iPhone/Android)
- [ ] Mobile menu functions
- [ ] Touch targets adequate (44x44)
- [ ] Forms usable on mobile
- [ ] Images properly sized
- [ ] No horizontal scroll
- [ ] Text readable without zoom

### Cross-Browser
- [ ] Chrome (latest)
- [ ] Firefox (latest)
- [ ] Safari (latest)
- [ ] Edge (latest)

### Performance
- [ ] Lighthouse score > 90
- [ ] Images optimized
- [ ] Scripts minified
- [ ] GZIP enabled

### Accessibility
- [ ] Keyboard navigation works
- [ ] Screen reader compatible
- [ ] Color contrast adequate
- [ ] Alt text on images
```

## 🔍 Debugging Failed Tests

### Common Issues:
1. **Timing**: Add `waitForSelector` for dynamic content
2. **Interactions**: Wait for Webflow animations
3. **CMS**: Content may vary between environments
4. **Forms**: Webflow forms require special handling

### Debug Mode:
```js
const browser = await puppeteer.launch({
  headless: false, // See what's happening
  slowMo: 250 // Slow down actions
});
```

## 🚀 Quick Start Testing Script

```bash
#!/bin/bash
# run-tests.sh

echo "🧪 Running Webflow Site Tests..."

# Basic checks
node tests/basic-checks.js

# Performance
node tests/performance.js

# Generate report
node tests/generate-report.js

echo "✅ Tests complete! Check test-report.html"
```

Remember: Since Webflow doesn't provide testing APIs, these external tools help ensure your custom code works correctly with the published site.