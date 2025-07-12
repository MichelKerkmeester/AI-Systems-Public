# /pr - JavaScript Documentation Best Practices

**Note**: This describes general documentation practices for JavaScript projects. Neither Webflow nor Slater provide native documentation generation - you'll use standard JS tooling.

---

## ⚡ Documentation Approaches
```bash
/pr jsdoc        # JSDoc setup and examples
/pr readme       # README.md template
/pr changelog    # Semantic versioning guide
/pr slater       # Document Slater code structure
```

---

## 📝 Setting Up Documentation

Since Slater is just a code editor, you'll handle documentation manually or with standard tools:

### 1. JSDoc Setup
```bash
# Install JSDoc locally
npm install --save-dev jsdoc

# Create config
echo '{
  "source": {
    "include": ["./src"],
    "includePattern": ".+\\.js$"
  },
  "opts": {
    "destination": "./docs"
  }
}' > jsdoc.json

# Generate docs
npx jsdoc -c jsdoc.json
```

### 2. Manual Documentation Structure
```
/docs
  ├── README.md          # Project overview
  ├── CHANGELOG.md       # Version history
  ├── modules/           # Module-specific docs
  │   ├── forms.md
  │   └── animations.md
  └── webflow-setup.md   # Webflow configuration guide
```

---

## 📚 Documentation Types

### 1. Module Documentation
```js
/**
 * Form Enhancement Module
 * @module form-enhance
 * @description Adds real-time validation to Webflow forms
 * 
 * @example
 * // Initialize on specific form
 * FormEnhance.init('[data-name="Contact Form"]');
 * 
 * @requires Webflow.push
 * @motion Motion.dev for error animations
 */
```

### 2. Function Documentation
```js
/**
 * Validates email format
 * @param {string} email - Email address to validate
 * @returns {boolean} True if valid email format
 * @throws {Error} If email parameter is not a string
 */
function validateEmail(email) {
  // Implementation
}
```

### 3. CSS Documentation
```css
/**
 * Form States
 * Enhanced states for form interactions
 * 
 * States:
 * - .is-validating: During validation
 * - .has-error: Validation failed
 * - .is-success: Validation passed
 * 
 * @group Forms
 * @since 1.2.0
 */
```

### 4. Webflow-Specific Documentation
```markdown
## Webflow Integration Guide

### Required Setup in Webflow Designer
Before using this code, ensure these elements exist:

**Forms**:
- Add form block with name "Contact Form"
- Set form name: `data-name="Contact Form"`
- Add email field with name "email"
- Include submit button with class `.submit-button`

**Attributes**:
- Form wrapper: `data-form-type="contact"`
- Error text: `.w-form-error` (Webflow default)
- Success message: `.w-form-done` (Webflow default)

### Slater Configuration
1. Create new file in Slater: `/forms/validation.js`
2. Set to load on: All pages (or specific)
3. Publish to: Development first, then Production

### Testing Instructions
1. Publish to Webflow staging
2. Test form submission
3. Verify error states
4. Check success message
```

---

## 🎯 README Structure
```markdown
# Project Name

## Overview
Brief description of enhancements added to Webflow site

## Features
- ✨ Real-time form validation
- 🎨 Smooth animations with Motion.dev
- 📱 Mobile-optimized interactions
- ♿ WCAG compliant

## Installation
1. Add to Slater
2. Configure Webflow elements
3. Deploy

## Usage
[Code examples]

## API Reference
[Generated from JSDoc]

## Performance
- Bundle size: 12.4kb (gzipped)
- Load time impact: < 50ms
- Animation: 60fps guaranteed
```

---

## 📊 Changelog Format
```markdown
## [1.2.0] - 2025-07-11

### Added
- Real-time email validation
- Error shake animation
- Success confirmation state

### Changed
- Migrated from GSAP to Motion.dev (mini)
- Improved mobile touch targets

### Fixed
- Form submission race condition
- Memory leak in event listeners

### Performance
- Reduced bundle by 8kb
- Improved FCP by 200ms
```

---

## 🔧 Practical Documentation Tools

### Documentation Generator Script
```js
// generate-docs.js
const fs = require('fs');
const path = require('path');

function generateModuleDocs(modulePath) {
  const code = fs.readFileSync(modulePath, 'utf8');
  const functionRegex = /\/\*\*([\s\S]*?)\*\/\s*function\s+(\w+)/g;
  
  let doc = `# ${path.basename(modulePath)}\n\n`;
  let match;
  
  while ((match = functionRegex.exec(code))) {
    const comment = match[1];
    const funcName = match[2];
    doc += `## ${funcName}\n${comment}\n\n`;
  }
  
  return doc;
}

// Run: node generate-docs.js
```

### VS Code Snippets for Documentation
```json
{
  "Webflow Module": {
    "prefix": "wfdoc",
    "body": [
      "/**",
      " * ${1:Module description}",
      " * @module ${2:moduleName}",
      " * @requires Webflow.push",
      " * ",
      " * @webflow-setup",
      " * - ${3:Required elements in Designer}",
      " * ",
      " * @example",
      " * ${4:Code example}",
      " */"
    ]
  }
}
```

---

## 💡 Documentation Reality Check

**What's Possible**:
✅ Manual documentation in Slater comments
✅ README.md in your Git repository  
✅ JSDoc comments (processed externally)
✅ Changelog tracking (manual or automated)
✅ VS Code snippets for consistency

**What's NOT Possible**:
❌ Auto-generation from Slater
❌ Native Webflow documentation features
❌ Integrated documentation viewer
❌ Automatic API reference generation
❌ Built-in version tracking

---

## 🚀 Quick Templates

### New Feature
```bash
/pr feature "Add smooth scroll"
# Generates: feature-smooth-scroll.md
```

### Bug Fix
```bash
/pr fix "Resolve CMS pagination"  
# Generates: fix-cms-pagination.md
```

### Refactor
```bash
/pr refactor "Optimize animations"
# Generates: refactor-animations.md
```

---

## 📍 Practical Workflow
```bash
# 1. Write code in Slater with good comments
# 2. Export to Git repository
# 3. Run documentation generation
npm run docs

# 4. Example package.json scripts
"scripts": {
  "docs": "jsdoc -c jsdoc.json",
  "changelog": "conventional-changelog -p angular -i CHANGELOG.md -s",
  "readme": "node generate-readme.js"
}
```

**Remember**: Documentation is a manual process. Neither Webflow nor Slater provide documentation generation features. Use standard JavaScript practices!