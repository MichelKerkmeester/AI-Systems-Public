# /pr - JavaScript Documentation Best Practices

**Note**: This describes general documentation practices for JavaScript projects. Neither Webflow nor Slater provide native documentation generation - you'll use standard JS tooling.

## 📚 Documentation Approaches

### 1. JSDoc Comments (Recommended)
**What**: Industry-standard inline documentation
**Why**: IDE support, type hints, auto-completion
**Effort**: Low - write as you code

```js
/**
 * Animates collection items with stagger effect
 * @param {HTMLElement} container - Collection list wrapper
 * @param {Object} options - Animation configuration
 * @param {number} [options.duration=0.6] - Animation duration in seconds
 * @param {number} [options.stagger=0.1] - Delay between items
 * @returns {Animation} Motion.dev animation instance
 * @example
 * animateCollection(document.querySelector('[data-collection="products"]'), {
 *   duration: 0.8,
 *   stagger: 0.15
 * });
 */
function animateCollection(container, options = {}) {
  // Implementation
}
```

### 2. README Documentation
**What**: Project overview and usage guide
**Why**: Quick onboarding, setup instructions
**Effort**: Medium - one-time setup

### 3. Code Comments
**What**: Inline explanations for complex logic
**Why**: Context for future developers (including yourself)
**Effort**: Low - add as needed

```js
// Reason: Webflow re-renders collection lists on filter change,
// so we need to re-attach our animations after DOM update
Webflow.push(() => {
  attachAnimations();
});
```

## 🛠️ Setting Up Documentation

### Step 1: Install JSDoc (Optional)
```bash
npm install --save-dev jsdoc
```

### Step 2: Add to package.json
```json
{
  "scripts": {
    "docs": "jsdoc -c jsdoc.json"
  }
}
```

### Step 3: Create jsdoc.json
```json
{
  "source": {
    "include": ["src"],
    "exclude": ["node_modules"]
  },
  "opts": {
    "destination": "./docs",
    "recurse": true
  }
}
```

## 📝 Documentation Types

### 1. Function Documentation
```js
/**
 * @function validateForm
 * @description Validates Webflow form before submission
 * @param {HTMLFormElement} form - Webflow form element
 * @returns {boolean} Validation result
 * @fires CustomEvent#formValidated
 * @since 1.0.0
 */
```

### 2. Module Documentation
```js
/**
 * @module animations/scroll
 * @description Scroll-triggered animations for Webflow elements
 * @requires motion.dev
 * @see {@link https://motion.dev/docs/scroll}
 */
```

### 3. Class Documentation
```js
/**
 * @class SliderController
 * @classdesc Manages Swiper.js integration with Webflow CMS
 * @param {HTMLElement} element - Slider container
 * @param {Object} config - Swiper configuration
 * @example
 * const slider = new SliderController(
 *   document.querySelector('[data-slider="hero"]'),
 *   { loop: true, autoplay: true }
 * );
 */
```

## 📋 README Structure

```markdown
# Project Name

Webflow custom code for [site name]

## 🚀 Quick Start

1. Clone repository
2. Install dependencies: `npm install`
3. Development: `npm run dev`
4. Build: `npm run build`

## 📁 Structure

```
src/
├── animations/     # Motion.dev animations
├── components/     # Interactive components
├── utils/         # Helper functions
└── main.js        # Entry point
```

## 🛠️ Features

- Smooth scroll animations
- Dynamic filtering
- Form validation
- Performance optimized

## 📝 Webflow Setup

1. Add to Site Settings > Custom Code > Footer:
```html
<script src="your-script.js"></script>
```

2. Required attributes:
- `data-animate="fade"` - Fade animations
- `data-slider="name"` - Slider instances

## ⚙️ Configuration

```js
window.SITE_CONFIG = {
  animations: {
    duration: 0.6,
    easing: 'ease-out'
  }
};
```

## 🐛 Known Issues

- Collection list animations reset on filter
- iOS Safari scroll performance

## 📄 License

MIT
```

## 🔄 Changelog Format

```markdown
# Changelog

## [1.2.0] - 2024-01-15
### Added
- Scroll-triggered animations
- Form validation

### Fixed
- Mobile menu z-index issue
- Collection list memory leak

### Changed
- Upgraded to Motion.dev 1.2
- Improved performance metrics
```

## 🎯 Practical Documentation

### What to Document
1. **Complex logic** - Why, not what
2. **Webflow workarounds** - Platform limitations
3. **Dependencies** - Version requirements
4. **Setup steps** - Attributes, classes needed
5. **Breaking changes** - Migration guides

### What NOT to Document
1. Obvious code (`// increment counter`)
2. Standard patterns
3. Webflow's own features

## 🚀 Quick Templates

### Function Template
```js
/**
 * Brief description
 * @param {Type} name - Description
 * @returns {Type} Description
 */
```

### Webflow Integration Template
```js
/**
 * Integrates with Webflow [feature]
 * @requires Webflow.push
 * @see https://university.webflow.com/
 * Note: [Any Webflow-specific limitations]
 */
```

## 💡 Documentation Tools

1. **VS Code Extensions**
   - Document This
   - Better Comments
   - JSDoc support

2. **Online Generators**
   - JSDoc Live: https://jsdoc.app/
   - TypeDoc (if using TypeScript)

3. **Validation**
   - ESLint JSDoc plugin
   - JSDoc linting

## ✅ Documentation Checklist

- [ ] All public functions have JSDoc
- [ ] README has setup instructions
- [ ] Complex logic has inline comments
- [ ] Webflow-specific notes included
- [ ] Examples provided for main features
- [ ] Dependencies and versions listed
- [ ] Known issues documented

## 🔧 Practical Workflow

1. **While coding**: Add JSDoc to functions
2. **After feature**: Update README features
3. **Before commit**: Check documentation
4. **On release**: Update changelog

## 📖 Documentation Reality Check

For Webflow projects, focus on:
1. **Setup instructions** (most important)
2. **Attribute requirements**
3. **Integration points**
4. **Troubleshooting guide**

Skip:
1. Generated API docs (overkill)
2. Extensive type definitions
3. Over-documenting simple code

Remember: Good documentation helps your future self and team members understand the "why" behind the code, especially with Webflow's unique constraints.