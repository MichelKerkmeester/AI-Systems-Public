# /wf-workflow - Complete Webflow + IDE Development Workflow

When you type `/wf-workflow`, I'll first ask:

## 🎯 Workflow Selection
```
"Which parts of the workflow do you need?

1. **Full Workflow** - All phases (Explore → Plan → Code → Test → Write Up)
2. **Explore Only** - Analyze existing code/structure
3. **Plan Only** - Create implementation plan
4. **Code → Test** - Implementation and validation
5. **Test → Write Up** - Validation and documentation
6. **Custom Selection** - Choose specific phases

Or describe your need: 'I need to plan a new feature' or 'Ready to code, skip exploration'"
```

## 📋 Custom Phase Selection
If you choose custom:
```
"Select the phases you need:
□ Explore - Analyze existing structure
□ Plan - Create detailed approach
□ Code - Implementation
□ Test - Validation
□ Write Up - Documentation

Example: 'Just Plan and Code' or 'Skip to Testing'"
```

## 🚀 Quick Starts
```
Common patterns:
- "New feature" → Full workflow
- "Bug fix" → Explore + Code + Test
- "Refactor" → Explore + Plan + Code
- "Documentation" → Test + Write Up
- "Quick change" → Code + Test only
```

---

## 🎯 Initial Assessment
After workflow selection:
```
"What are we building/fixing?
- New feature/component
- Complex JavaScript functionality
- Fixing an issue
- Performance optimization
- Redesigning existing element
- Adding custom functionality

Describe the requirements and I'll orchestrate your selected workflow."
```

## 🖥️ Development Environment
```
Your workflow:
IDE (JavaScript Development) → Webflow (Visual Development + Custom Code)
```

## 📌 Phase Execution
Based on your selection, I'll execute only the chosen phases:

### If Starting Mid-Workflow
```
"I notice you're starting with [Phase].
Do you want me to:
1. Assume exploration is done
2. Use existing plan/documentation
3. Quick review what we're working on

This helps me provide better context."
```

### Phase Transitions
```
After each phase:
"✅ [Phase] Complete!
Continue to [Next Phase] or stop here?"

This allows flexibility to:
- Add phases you initially skipped
- Stop when you have what you need
- Adjust based on findings
```

---

## 📍 Phase 1: EXPLORE

### Parallel Exploration
```
"Starting comprehensive exploration...

Spawning 5 parallel agents:
- Agent 1: Analyzing all pages using similar components
- Agent 2: Checking existing Slater scripts for patterns
- Agent 3: Reviewing CMS structure and dependencies
- Agent 4: Documenting current interactions/animations
- Agent 5: Identifying reusable symbols and classes

This will map everything relevant to your requirement."
```

### Exploration Targets

#### IDE Code Structure
```
Files to analyze:
- Existing JavaScript modules
- Utility functions and helpers
- Similar feature implementations
- Test files (if applicable)
```

#### Webflow Structure
```
Pages to analyze:
- Which pages have similar functionality?
- What symbols could be reused/modified?
- Which classes follow the pattern we need?

Components to check:
- Existing interactions that could be adapted
- Custom code blocks that solve similar problems
- CMS collections that might be affected
```

### Exploration Output
```markdown
### 📊 Exploration Results

**IDE Findings:**
- Relevant modules: [file paths]
- Reusable utilities: [function names]
- Similar patterns in: [files]
- Test coverage: [if applicable]

**Webflow Findings:**
- Found 3 similar components on: [pages]
- Reusable symbol: [symbol-name] needs minor modifications
- CSS classes to leverage: [.class-names]
- Custom code locations: [page settings/project settings]

**Edit Targets:**
- IDE files: [specific modules to modify]
- Webflow pages: [pages to update]
- Custom code areas: [where to add/modify code]
```

---

## 📋 Phase 2: PLAN

### Detailed Planning Process
```
"Based on exploration, creating implementation plan...

Analyzing:
- Can this be CSS-only? (/wf-css-first)
- What's the minimum JS needed?
- Which approach has best performance?
- What are the Webflow constraints?"
```

### Research Phase
```
"I need to research these unknowns:

Spawning research agents for:
- Browser support for [CSS feature]
- Webflow limitations for [functionality]
- Best practices for [specific technique]
- Performance impact of [approach]

(~3k tokens)"
```

### ⏸️ Planning Checkpoint
```
"Before proceeding, I need clarification:

1. [Specific question about requirement]
2. [Tradeoff decision needed]
3. [Constraint to confirm]

Please provide input so I can finalize the plan."
```

### Implementation Plan
```markdown
## Implementation Plan: [Feature Name]

### Overview
- Approach: [CSS-first with modular JS]
- Development: IDE → Webflow Custom Code
- Complexity: [Low/Medium/High]
- Time Estimate: [X hours]
- Risk Level: [Low/Medium/High]

### Phase 1: Code Architecture (IDE)
1. [ ] Create/modify modules: [list]
   - File structure
   - Export/import strategy
2. [ ] Write core functionality
   - Pure functions first
   - Event handlers separate
3. [ ] Add error handling
4. [ ] Write tests (optional)

### Phase 2: Visual Foundation (Webflow)
1. [ ] Create/modify symbol: [name]
   - Add classes: [list]
   - Structure: [HTML hierarchy]
2. [ ] Set up responsive behavior
   - Desktop: [approach]
   - Tablet: [approach]
   - Mobile: [approach]

### Phase 3: Styling (CSS)
1. [ ] Custom CSS in Webflow:
   ```css
   /* Example structure */
   .component-name {
     /* Base styles */
   }
   ```
2. [ ] Interactions (Webflow native):
   - Trigger: [hover/click/scroll]
   - Animation: [transform/opacity]

### Phase 4: Integration (Webflow Custom Code)
1. [ ] Add JavaScript to Webflow:
   - Location: [Page Settings/Project Settings]
   - Load order: [before </body> or in <head>]
2. [ ] Bundle/minify code from IDE
3. [ ] Set up initialization:
   ```javascript
   // Integration pattern
   Webflow.push(() => {
     initializeComponent();
   });
   ```

### Testing Strategy
- [ ] Desktop browsers: Chrome, Safari, Firefox
- [ ] Mobile: iOS Safari, Chrome Android
- [ ] Interactions: All triggers work
- [ ] Performance: No CLS, smooth animations
- [ ] Accessibility: Keyboard nav, screen readers

### Documentation Plan
- [ ] Update style guide
- [ ] Document component usage
- [ ] Add Slater script comments
- [ ] Create example in style guide

---

## 💻 Phase 3: CODE

### Pre-Code Checklist
```
"Before coding, confirming:
✓ IDE environment ready
✓ Webflow Designer is ready
✓ Custom code locations identified
✓ Backup created
✓ Development domain active

Starting implementation..."
```

### Coding Standards

#### IDE JavaScript Best Practices
```javascript
// ESLint + Prettier configured
// Clear naming conventions
const sliderComponent = {
  init() {
    this.cacheDOM();
    this.bindEvents();
  },
  
  cacheDOM() {
    this.slider = document.querySelector('.slider');
    this.slides = [...this.slider.children];
  }
};

// Modular structure
export { sliderComponent };
```

#### Webflow Best Practices
```
Naming Conventions:
- Classes: .component-name__element--modifier
- Symbols: Component - Variant
- Interactions: Descriptive names

Structure:
- Semantic HTML
- Minimal nesting
- Reusable classes
```

#### Slater Code Style
```javascript
// Clear variable names over comments
const heroSlider = document.querySelector('.hero-slider');
const slideCount = heroSlider.children.length;

// Event delegation over multiple listeners
document.addEventListener('click', (e) => {
  if (e.target.matches('.slider-nav')) {
    handleSliderNav(e);
  }
});

// Webflow-aware initialization
Webflow.push(() => {
  initializeComponent();
});
```

### Progressive Implementation
```
"Implementing in stages:

1. JavaScript Development (IDE)
   - Write modular code
   - Run linting/formatting
   - Test locally if needed
   
2. Code Preparation
   - Bundle/minify if needed
   - Prepare for Webflow integration
   - Document dependencies
   
3. Webflow Structure (Designer)
   - Create base HTML
   - Add semantic classes
   
4. Styling (Designer + Custom CSS)
   - Visual design
   - Responsive behavior
   
5. Integration (Custom Code)
   - Add JS to Page/Project Settings
   - Test functionality
   - Check console for errors"
```

### Deployment Workflow
```bash
# After IDE development
1. Run linting: npm run lint
2. Run formatter: npm run format
3. Bundle/build: npm run build
4. Copy to Webflow custom code
5. Test in Webflow preview
```

### Code Validation
```
After each stage:
- Preview on all breakpoints
- Check console for errors
- Validate accessibility
- Test interactions
```

---

## 🧪 Phase 4: TEST

### Automated Testing
```
"Running validation suite...

1. Quick validation (/wf-validate quick)
   - Console errors: [status]
   - Basic accessibility: [status]
   
2. Performance check
   - PageSpeed Insights: [score]
   - Core Web Vitals: [metrics]
   
3. Cross-browser testing
   - Desktop: [results]
   - Mobile: [results]"
```

### Manual Testing Checklist
```
Functionality:
□ All interactions work as designed
□ Forms submit correctly
□ CMS filtering works
□ Animations smooth (60fps)
□ No layout shifts

Edge Cases:
□ Empty states handled
□ Long text doesn't break layout
□ Works without JavaScript
□ Handles slow connections
□ Respects reduced motion
```

### Testing Issues Found
```
"⚠️ Issues discovered:

1. [Issue]: [Description]
   - Impact: [Low/Medium/High]
   - Fix: [Proposed solution]

Returning to PLAN phase to address..."
```

---

## 📝 Phase 5: WRITE UP

### Documentation Output
```markdown
## Feature Implementation: [Name]

### What Was Built
[2-3 sentences describing the feature and its purpose]

### Technical Approach
- Chose [approach] because [reasoning]
- Developed in IDE for [code quality/testing/reusability]
- Used CSS for [list] to maintain performance
- Integrated via Webflow custom code for [simplicity/control]

### Implementation Details

**IDE Code Structure:**
- New modules: [list with file paths]
- Utilities added: [functions and purpose]
- Dependencies: [external libraries if any]
- Tests: [if applicable]

**Webflow Integration:**
- Custom code location: [Page/Project Settings]
- Load timing: [before </body> or <head>]
- File size: [minified size]

**Webflow Structure:**
- New/Modified Symbols: [list with purpose]
- Custom Classes: [list with naming convention]
- Interactions: [list with triggers]

**Integration Points:**
- Webflow.push() usage: [where and why]
- Event listeners: [what they monitor]
- DOM queries: [selectors used]

**Performance Impact:**
- Before: [metrics]
- After: [metrics]
- Improvement: [percentage/ms]

### Usage Instructions
1. For developers:
   - IDE files located at: [path]
   - To modify: edit [files] and rebuild
   - Run build process before deploying

2. For Webflow editors:
   - To implement on new page:
     - Add symbol [name]
     - Include class [class]
     - Ensure custom code is added to [location]

### Testing Performed
- ✅ ESLint: [pass/fixed issues]
- ✅ Local testing: [what was tested]
- ✅ PageSpeed: [score]
- ✅ Cross-browser: [browsers tested]
- ✅ Mobile: Fully responsive

### Development Notes
- IDE setup required: [tools/config]
- Build process: [commands]
- Known limitations: [list]
- Future enhancements: [list]
```

---

## 🔄 Workflow Summary

### Complete Process (When Selected)
```
1. EXPLORE: Analyze IDE codebase + Webflow structure
2. PLAN: Architecture design + visual planning
3. CODE: IDE development → Webflow custom code integration
4. TEST: Code quality + visual validation
5. WRITE UP: Technical docs + usage guide

Total time: [varies by phases selected]
Token usage: 
- Single phase: ~3-5k
- Two phases: ~8-10k
- Full workflow: ~15-25k
```

### Phase Dependencies
```
⚠️ Recommended sequences:
- Plan requires: Explore (or existing knowledge)
- Code requires: Plan (or clear requirements)
- Test requires: Code (or existing implementation)
- Write Up benefits from: Test results

You can skip phases, but I'll note if you're missing helpful context.
```

### Development Pipeline
```
IDE (Develop) → Build/Bundle → Webflow (Custom Code) → Live Site
      ↓              ↓                   ↓                ↓
 Lint/Format    Minify/Optimize    Visual Test      Production
```

### Quick Mode Examples
```
"/wf-workflow explore" - Just exploration
"/wf-workflow plan-only" - Skip to planning
"/wf-workflow test" - Jump to validation
"/wf-workflow quick-fix" - Code + Test only
```

💡 **Tip**: This modular approach saves tokens and time by focusing only on what you need right now.