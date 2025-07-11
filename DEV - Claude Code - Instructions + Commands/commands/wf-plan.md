# /wf-plan - CSS-First Implementation Planning

When you type `/wf-plan`, create detailed implementation plan:

## 📝 Markdown Scratchpad
For complex features, create `PLAN.md`:
```markdown
## Feature: [Name]
### Exploration Results
- [Summary from /wf-explore]

### Implementation Approach
- [ ] CSS-only solution
- [ ] Required JS (minimal)
- [ ] Performance impact
```

## Checklist
- [ ] **Scope**: Exact Webflow elements changing (from exploration)
- [ ] **Dependencies**: Affected symbols, pages, CMS items
- [ ] **CSS Solution**: Can this be done without JS? `/wf-css-first`
- [ ] **Performance**: Impact on metrics (CLS, LCP) - current vs projected
- [ ] **Accessibility**: Keyboard nav, screen readers, WCAG 2.1 AA
- [ ] **Breakpoints**: Mobile-first approach (375px → 2560px)
- [ ] **Fallbacks**: Progressive enhancement strategy
- [ ] **Constraints**: Webflow limits identified in `/wf-risk`

## 🔍 Research Needed?
If uncertain, spawn agents for web research:
"I need to research [browser support for X]"

## ⏸️ Pause Checkpoint
Before proceeding, ask:
"I've identified [approach]. Should I explore [alternative] instead?"

## Output
```markdown
### Implementation Plan: [Feature Name]
**Approach**: CSS-only with [specific techniques]
**Fallback**: [Progressive enhancement details]
**Performance**: Expected [X]ms improvement
**Risk**: [Main concern] - Mitigation: [Strategy]
**Timeline**: [X] hours estimated
```

## Two-Claude Verification
For critical features: "Run `/wf-verify` to have another Claude review this plan"

## Next Step
Get approval → Implement → Use `/wf-test` continuously