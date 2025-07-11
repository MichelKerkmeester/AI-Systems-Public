# /wf-workflow - JavaScript & CSS Development Workflow

When you type `/wf-workflow`, I'll ask:

## 🎯 What code do you need?
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

## 📍 Phase 1: EXPLORE
Analyze existing code and Webflow integration points, use parallel subagents.

### What I'll explore:
- **JavaScript codebase**: Modules, utilities, patterns
- **Webflow selectors**: Available classes and data attributes
- **Event targets**: Forms, buttons, interactive elements
- **Dependencies**: Existing libraries and helpers

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
```

**Note**: I analyze but don't modify Webflow structure.

---

## 📋 Phase 2: PLAN
Design JavaScript architecture for existing Webflow elements.

**Notice**: If there are things you are not sure about, use parallel subagents to do some web research. They should only return useful information, no noise.

### Planning includes:
- Which Webflow elements to target
- Event handling strategy
- State management approach
- Performance considerations
- Webflow.js integration points

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

**Constraints**:
- Work with existing Webflow form structure
- Preserve Webflow's native form handling
- Add validation layer only
```

**Key principle**: Enhance, don't replace Webflow functionality.

---

## 💻 Phase 3: CODE
Write JavaScript and CSS that enhances existing Webflow elements. Follow the style of the existing codebase in the IDE

### Development approach:

1. **CSS Styling (when needed)**
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
   
   /* Respect Webflow breakpoints */
   @media (max-width: 991px) { /* Tablet */ }
   @media (max-width: 767px) { /* Mobile landscape */ }
   @media (max-width: 479px) { /* Mobile portrait */ }
   ```

2. **JavaScript Enhancement**
   ```javascript
   // Target Webflow's structure
   const forms = document.querySelectorAll('[data-name="Contact Form"]');
   
   // Add classes defined in your CSS
   function showError(element) {
     element.classList.add('form-error-state');
   }
   ```

3. **Integration Pattern**
- Slater autoloads - never add `DOMContentLoaded` listeners.
- Execute code directly or via `Webflow.push()` for Webflow-dependent features.

   ```javascript
   // CSS + JS working together
   Webflow.push(() => {
     // Apply custom styles dynamically
     loadCustomStyles();
     // Initialize JavaScript
     initEnhancements();
   });
   ```

### What I code:
✅ Custom CSS for specific styling needs
✅ CSS animations and transitions
✅ JavaScript event handlers
✅ API integrations
✅ Dynamic class toggling
✅ State management

### What I DON'T code:
❌ Webflow Designer changes
❌ Modifying core Webflow classes
❌ Creating symbols or components
❌ Changing HTML structure

---

## 🚀 Workflow Summary

### Core Development Process
```
1. EXPLORE: Analyze existing code and Webflow elements
2. PLAN: Design JavaScript architecture 
3. CODE: Implement enhancements

Total time: 45-60 min
Token usage: ~8-12k
```

### My Role: JavaScript & CSS Developer
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

### Quick commands:
```
/wf-workflow explore - Just analyze what exists
/wf-workflow plan    - Skip to architecture planning
/wf-workflow code    - Jump straight to implementation
```

### Prerequisites from Webflow team:
Before I can code, ensure:
1. Webflow structure is complete
2. Classes and data attributes are added
3. Interactions are configured
4. CMS collections are set up

💡 **Best practice**: Add `data-*` attributes to Webflow elements specifically for JavaScript targeting. This keeps styling and functionality separate.
