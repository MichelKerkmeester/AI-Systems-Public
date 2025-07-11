# /wf-workflow - JavaScript & CSS Development Workflow

When you type `/wf-workflow`, I'll ask:

## ⁉️ What code do you need?
```
1. **New Feature** - Add JavaScript/CSS to enhance Webflow
2. **Fix/Update** - Modify existing code
3. **Styling** - Custom CSS for specific needs
4. **Integration** - Connect to APIs or external services
5. **Quick Enhancement** - Simple handlers or animations

Example: "Add custom form validation with error styling" → New Feature
```

**Important**: I write JavaScript and CSS in the IDE only. Webflow visual structure must already exist.

---

## 🎯 Workflow Summary

### Core Development Process
```
1. EXPLORE: Analyze existing code and Webflow elements (parallel analysis)
2. PLAN: Design JavaScript architecture (parallel research when needed)
3. CODE: Implement enhancements with proper technical execution
```

### Quick commands:
```
/wf-workflow explore - Just analyze what exists (use when inheriting existing code)
/wf-workflow plan    - Skip to architecture planning (when you know the codebase)
/wf-workflow code    - Jump straight to implementation (for simple enhancements)
```

### 👨🏻My Role: JavaScript & CSS Developer
```
What I do:
✅ Write JavaScript modules in IDE
✅ Write custom CSS when needed
✅ Enhance existing Webflow functionality  
✅ Create animations and transitions (CSS/JS)
✅ Handle complex logic and integrations
✅ Style dynamic states and interactions

What I DON'T do:
❌ Work in Webflow Designer
❌ Create Webflow symbols or components
❌ Modify HTML structure
❌ Change core Webflow classes
❌ Build visual layouts
```

### 🏎️ Efficiency First
**For maximum efficiency, whenever performing multiple independent operations, invoke all relevant tools simultaneously rather than sequentially.**

This applies to:
- Exploring multiple code files
- Researching different libraries
- Checking various documentation sources
- Analyzing different aspects of the codebase

### Prerequisites from Webflow team:
Before I can code, ensure:
1. Webflow structure is complete
2. Classes and data attributes are added
3. Interactions are configured
4. CMS collections are set up

💡 **Best practice**: Add `data-*` attributes to Webflow elements specifically for JavaScript targeting. This keeps styling and functionality separate.

---

## 📍 Phase 1: EXPLORE
Analyze existing code and Webflow integration points.

### 🏎️ What I'll explore (in parallel):
- **JavaScript codebase**: Modules, utilities, patterns
- **Webflow selectors**: Available classes and data attributes
- **Event targets**: Forms, buttons, interactive elements
- **Dependencies**: Existing libraries and helpers

### Constraint Check:
- ✅ Identify existing Webflow structure (don't plan to modify)
- ✅ Note available classes and data attributes
- ❌ Flag any elements that would require DOM changes
- 📖 See FORBIDDEN PATTERNS in main system instructions

### Output example:
```
Found in code:
- Form handler: /modules/forms.js
- Utility functions: debounce(), throttle()
- Event patterns: delegation used throughout

Found in Webflow:
- Forms: .w-form, [data-name="Email Form"]
- CTAs: .button.primary, [data-action="submit"]
- Containers: .section[data-section-id]

Constraint flags:
- ✅ All target elements have proper selectors
- ⚠️ Modal structure might need data attributes added
```

**Note**: I analyze but don't modify Webflow structure.

---

## 📋 Phase 2: PLAN
Design JavaScript architecture for existing Webflow elements.

### Planning includes:
- Which Webflow elements to target
- Event handling strategy
- State management approach
- Performance considerations

### Constraint Validation:
- Verify approach uses only existing DOM structure
- Confirm no pixel units in CSS plans
- Check for Webflow.push() usage for dependent features
- Ensure no global namespace pollution
- 📖 Cross-check with FORBIDDEN PATTERNS

### 🏎️ Efficiency Principle:
If there are things you are not sure about, use parallel subagents to do web research simultaneously. Multiple independent research queries should be executed in parallel for maximum efficiency.

### MCP Tool Usage in Planning:
```javascript
// Parallel research for complex features
await Promise.all([
  invoke('context7', { library: 'gsap', topic: 'scrollTrigger' }),
  invoke('web_search', { query: 'Webflow CMS re-render events' }),
  invoke('sequential-thinking', { task: 'plan user interaction flow' })
]);
```

### Output format:
```markdown
## Plan: Form Enhancement Module

**Target elements**: 
- Forms: [data-name="Contact Form"]
- Submit buttons: .submit-button
- Error displays: .w-form-error

**Architecture**:
- /modules/form-enhance.js - Main logic
- /utils/validation.js - Validators
- /config/messages.js - Error messages

**Integration**: 
- Init via Webflow.push()
- Progressive enhancement (works without JS)
- No DOM structure changes

**Constraints verified**:
- ✅ Working with existing Webflow form structure
- ✅ Using REM units for any CSS
- ✅ Module pattern prevents global pollution
- ✅ Preserving Webflow's native form handling
```

**Key principle**: Enhance, don't replace Webflow functionality.

---

## 💻 Phase 3: CODE
Write JavaScript and CSS that enhances existing Webflow elements. Follow the style of the existing codebase in the IDE

### Pre-Implementation Checklist:
- [ ] No DOM structure modifications
- [ ] Using REM units, not pixels
- [ ] Using document.querySelector with existence checks
- [ ] Respecting reduced motion preferences
- [ ] 📖 Final review against FORBIDDEN PATTERNS

### Technical Execution Approach:

1. **General Principles**:
   - Bind events with `document.querySelector`
   - Start with CSS transitions; escalate only if needed
   - Respect reduced motion in all animations
   - Use will-change sparingly; remove after animation
   - Batch DOM updates in animation loops

2. **CSS Styling (when needed)**
   ```css
   /* Target existing Webflow classes */
   .w-form.contact-form {
     /* Custom enhancements */
   }
   
   /* Add new utility classes */
   .form-error-state {
     border-color: #e74c3c;
     animation: shake 0.3s;
   }
   ```

3. **JavaScript Enhancement**
   ```javascript
   // Use vanilla ES6+ exclusively
   const forms = document.querySelectorAll('[data-name="Contact Form"]');
   
   // Check element exists before using
   if (forms.length) {
     forms.forEach(form => {
       // Add classes defined in your CSS
       form.classList.add('enhanced-form');
     });
   }
   
   // For Collection Lists
   const items = document.querySelectorAll('.w-dyn-item');
   items.forEach(item => {
     item.dataset.animated = 'true'; // Custom data attribute for hooks
   });
   ```

4. **Integration Pattern**
   - Slater autoloads - never add `DOMContentLoaded` listeners
   - Execute code directly or via `Webflow.push()` for Webflow-dependent features
   - Use Motion.dev for modern animations (CDN or bundled)
   - Use GSAP for complex timelines (Webflow-owned, deep integration)

   ```javascript
   // Direct execution for non-Webflow dependent code
   initializeEnhancements();
   
   // Use Webflow.push for Webflow-specific features
   Webflow.push(() => {
     // Re-attach animations after CMS re-render
     reInitializeCollectionAnimations();
   });
   
   // Motion.dev via CDN (Webflow-friendly)
   import { animate } from "https://cdn.jsdelivr.net/npm/motion@11/mini/+esm"
   animate("header", { opacity: 1 })
   ```

### What I code:
✅ Custom CSS for specific styling needs
✅ CSS animations and transitions
✅ JavaScript event handlers
✅ API integrations
✅ Dynamic class toggling
✅ State management
✅ Collection List animations with proper re-attachment

### What I DON'T code:
❌ Webflow Designer changes
❌ Modifying core Webflow classes
❌ Creating symbols or components
❌ Changing HTML structure

---

## 🔧 MCP Tool Integration

Throughout the workflow, use MCP tools efficiently:
- **Explore phase**: Parallel analysis of code and documentation
- **Plan phase**: Simultaneous research and architecture design
- **Code phase**: Quick syntax checks and optimization

See `/wf-mcp` for detailed tool usage patterns.