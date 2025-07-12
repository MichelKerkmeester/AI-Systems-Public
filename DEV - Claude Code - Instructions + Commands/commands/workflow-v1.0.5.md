# /workflow - JavaScript Enhancement Workflow for Webflow

**Core Principle**: You're enhancing Webflow sites with JavaScript, not replacing them. Work within Webflow's constraints to add functionality.

## ⚡ Command Usage
```bash
/workflow explore  # Understand current setup
/workflow plan     # Design JS architecture  
/workflow code     # Implementation guide
```

---

## 📊 PHASE 1: EXPLORE (Understand Constraints)

### 1.1 Analyze Webflow Structure
```js
// Run these checks first
Promise.all([
  checkWebflowElements(),    // What exists in Designer
  checkExistingScripts(),    // Current custom code
  checkCMSStructure(),       // Collections & fields
  checkInteractions()        // Native Webflow animations
]);
```

### 1.2 Key Questions to Answer
- **What can't change?** (DOM structure from Webflow)
- **What's already animated?** (Don't duplicate Webflow interactions)
- **Where's the data?** (CMS collections, attributes)
- **What are the limits?** (Page count, CMS items, file sizes)

### 1.3 Exploration Checklist
```markdown
## Webflow Constraints Found:
- [ ] Collection Lists: ________________
- [ ] Forms: __________________________
- [ ] Native Interactions: _____________
- [ ] CMS Fields: _____________________
- [ ] Page Count: _____________________
- [ ] Current Custom Code: _____________
```

### 1.4 Code Discovery Pattern
```js
// Discover Webflow elements programmatically
const discovery = {
  collections: document.querySelectorAll('.w-dyn-list'),
  forms: document.querySelectorAll('form[data-name]'),
  cmsItems: document.querySelectorAll('.w-dyn-item'),
  richText: document.querySelectorAll('.w-richtext'),
  lightboxes: document.querySelectorAll('.w-lightbox'),
  sliders: document.querySelectorAll('.w-slider')
};

console.table(discovery);
```

---

## 🎯 PHASE 2: PLAN (Design JS Architecture)

### 2.1 Architecture Principles
1. **Enhance, don't replace** - Add to Webflow's functionality
2. **Data attributes over classes** - Classes change in Designer
3. **Progressive enhancement** - Site works without JS
4. **Webflow.push() for timing** - Ensure Webflow loads first

### 2.2 Module Structure
```
project/
├── animations/
│   ├── scroll.js      # Scroll-triggered animations
│   ├── hover.js       # Enhanced hover states
│   └── loader.js      # Page transitions
├── components/
│   ├── filters.js     # CMS filtering
│   ├── search.js      # Real-time search
│   └── forms.js       # Form validation
├── utils/
│   ├── webflow.js     # Webflow helpers
│   ├── dom.js         # DOM utilities
│   └── performance.js # Optimization helpers
└── main.js            # Entry point
```

### 2.3 Integration Planning
```js
// Plan your data attributes
const dataAttributes = {
  // Components
  'data-component': ['nav', 'filter', 'search', 'form'],
  
  // Animations
  'data-animate': ['fade', 'slide', 'scale', 'parallax'],
  
  // Interactions
  'data-trigger': ['click', 'hover', 'scroll', 'load'],
  
  // State
  'data-state': ['active', 'loading', 'error', 'success']
};
```

### 2.4 Performance Budget
```js
const performanceBudget = {
  jsSize: '50kb',          // Minified + gzipped
  loadTime: '100ms',       // Script execution
  fps: 60,                 // Animation target
  interactions: '16ms'     // Response time
};
```

---

## 💻 PHASE 3: CODE (Implementation)

### 3.1 Webflow-Safe Initialization
```js
// main.js - Entry point
(() => {
  'use strict';
  
  // Feature detection
  if (!window.Webflow) {
    console.warn('Webflow not detected');
    return;
  }
  
  // Wait for Webflow
  window.Webflow.push(() => {
    initializeEnhancements();
  });
  
  function initializeEnhancements() {
    // Check for required elements
    const hasCollections = document.querySelector('.w-dyn-list');
    const hasForms = document.querySelector('form[data-name]');
    
    // Initialize modules conditionally
    if (hasCollections) {
      import('./components/filters.js').then(m => m.init());
    }
    
    if (hasForms) {
      import('./components/forms.js').then(m => m.init());
    }
    
    // Always initialize animations
    import('./animations/scroll.js').then(m => m.init());
  }
})();
```

### 3.2 Working with Collections
```js
// components/filters.js
export function init() {
  const filterButtons = document.querySelectorAll('[data-filter]');
  const collection = document.querySelector('[data-collection]');
  
  if (!filterButtons.length || !collection) return;
  
  // Store original items (Webflow will modify DOM)
  const items = [...collection.querySelectorAll('.w-dyn-item')];
  
  filterButtons.forEach(button => {
    button.addEventListener('click', (e) => {
      const filter = e.target.dataset.filter;
      
      // Let Webflow handle the filtering
      // Just enhance with animations
      items.forEach(item => {
        if (shouldShow(item, filter)) {
          animateIn(item);
        } else {
          animateOut(item);
        }
      });
    });
  });
}
```

### 3.3 Form Enhancements
```js
// components/forms.js
export function init() {
  const forms = document.querySelectorAll('form[data-name]');
  
  forms.forEach(form => {
    // Don't interfere with Webflow's submission
    form.addEventListener('submit', async (e) => {
      // Add loading state
      form.dataset.state = 'loading';
      
      // Let Webflow handle the actual submission
      // Just provide visual feedback
    });
    
    // Enhance with real-time validation
    const inputs = form.querySelectorAll('input, textarea');
    inputs.forEach(input => {
      input.addEventListener('blur', () => validateField(input));
    });
  });
}
```

### 3.4 Animation Integration
```js
// animations/scroll.js
import { animate, scroll } from 'motion.dev';

export function init() {
  // Find elements to animate
  const elements = document.querySelectorAll('[data-animate]');
  
  elements.forEach(element => {
    const type = element.dataset.animate;
    
    // Don't animate if Webflow already is
    if (element.classList.contains('w-ix-trigger')) {
      console.warn('Element already has Webflow interaction');
      return;
    }
    
    // Apply animation based on type
    switch(type) {
      case 'fade':
        scroll(animate(element, {
          opacity: [0, 1],
          transform: ['translateY(20px)', 'translateY(0)']
        }), {
          target: element,
          offset: ['start end', 'end start']
        });
        break;
    }
  });
}
```

### 3.5 Performance Optimization
```js
// utils/performance.js
export const debounce = (func, wait) => {
  let timeout;
  return (...args) => {
    clearTimeout(timeout);
    timeout = setTimeout(() => func.apply(this, args), wait);
  };
};

export const throttle = (func, limit) => {
  let inThrottle;
  return (...args) => {
    if (!inThrottle) {
      func.apply(this, args);
      inThrottle = true;
      setTimeout(() => inThrottle = false, limit);
    }
  };
};

// Use with scroll events
window.addEventListener('scroll', throttle(handleScroll, 16));
```

### 3.6 Webflow Helpers
```js
// utils/webflow.js
export const webflowReady = () => {
  return new Promise(resolve => {
    if (window.Webflow && window.Webflow.push) {
      window.Webflow.push(resolve);
    } else {
      document.addEventListener('DOMContentLoaded', resolve);
    }
  });
};

export const refreshWebflow = () => {
  window.Webflow && window.Webflow.ready();
};

export const destroyWebflow = () => {
  window.Webflow && window.Webflow.destroy();
};

export const reinitWebflow = () => {
  destroyWebflow();
  refreshWebflow();
};
```

---

## 🎯 Common Patterns

### Pattern 1: Enhanced Filtering
```js
// Webflow provides basic filtering, we add:
// - Smooth transitions
// - Multiple filter combinations  
// - Result count
// - No results state
```

### Pattern 2: Smooth Scroll
```js
// Webflow has basic anchor links, we enhance:
// - Offset for fixed headers
// - Smooth easing
// - Progress indicators
// - Section highlighting
```

### Pattern 3: Form Validation
```js
// Webflow validates on submit, we add:
// - Real-time field validation
// - Custom error messages
// - Progress indicators
// - Success animations
```

### Pattern 4: Dynamic Content
```js
// Webflow CMS is static, we enable:
// - Load more buttons
// - Infinite scroll
// - Real-time search
// - Dynamic sorting
```

---

## ⚠️ Critical Gotchas

### 1. Collection List Re-rendering
```js
// Problem: Webflow rebuilds DOM on filter
// Solution: Use MutationObserver
const observer = new MutationObserver(() => {
  reattachListeners();
});

observer.observe(collectionList, {
  childList: true,
  subtree: true
});
```

### 2. Form Submission
```js
// Problem: Can't prevent Webflow submission
// Solution: Use form states
form.addEventListener('submit', () => {
  // Don't e.preventDefault()!
  // Just add visual feedback
  form.classList.add('is-submitting');
});
```

### 3. Responsive Images
```js
// Problem: Webflow uses responsive images
// Solution: Wait for load
const images = element.querySelectorAll('img');
const imagePromises = [...images].map(img => {
  return new Promise(resolve => {
    if (img.complete) resolve();
    else img.onload = resolve;
  });
});

await Promise.all(imagePromises);
```

### 4. Designer Preview
```js
// Problem: Code runs in Designer
// Solution: Detect environment
const isDesigner = window.location.href.includes('webflow.io');
if (isDesigner) {
  console.log('Running in Designer - limited functionality');
}
```

---

## 📋 Deployment Checklist

### Pre-deployment:
- [ ] Remove all console.log statements
- [ ] Minify JavaScript files
- [ ] Test on published site (not just Designer)
- [ ] Check mobile devices
- [ ] Validate no layout shifts
- [ ] Ensure progressive enhancement
- [ ] Document data attributes needed

### Slater Integration:
```js
// Slater auto-loads, so just:
// 1. Upload to Slater
// 2. Add Slater snippet to Webflow
// 3. No DOMContentLoaded needed!
```

### Performance Metrics:
- First Input Delay < 100ms
- No layout shifts from JS
- 60 FPS animations
- < 50KB total JS size

---

## 🚀 Quick Start Templates

### Template 1: Basic Enhancement
```js
// Minimal Webflow enhancement setup
(() => {
  'use strict';
  
  window.Webflow.push(() => {
    console.log('Enhancing Webflow site...');
    
    // Your code here
  });
})();
```

### Template 2: Module Loader
```js
// Dynamic module loading based on page elements
const modules = [
  { selector: '[data-filter]', path: './filters.js' },
  { selector: '[data-animate]', path: './animations.js' },
  { selector: '[data-search]', path: './search.js' }
];

modules.forEach(({ selector, path }) => {
  if (document.querySelector(selector)) {
    import(path).then(m => m.init());
  }
});
```

### Template 3: Component Base
```js
// Base component class
class WebflowComponent {
  constructor(element) {
    this.element = element;
    this.init();
  }
  
  init() {
    // Override in subclass
  }
  
  destroy() {
    // Cleanup
  }
}
```

Remember: Your JavaScript enhances Webflow's functionality. Always respect the platform's constraints and work with them, not against them.