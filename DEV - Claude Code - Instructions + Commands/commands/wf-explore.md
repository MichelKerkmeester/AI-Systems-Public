# /wf-explore - Modular Webflow Exploration

When you type `/wf-explore`, I'll first ask:

## 🎯 Exploration Options
```
"What would you like me to explore? Choose one or multiple:

1. **Structure** - Pages, symbols, components, interactions
2. **CMS** - Collections, fields, references, limits
3. **Styles** - Classes, custom properties, breakpoints
4. **Code** - Slater scripts, embeds, custom CSS/JS
5. **Performance** - Image sizes, fonts, script impact
6. **Specific Component** - Deep dive on one element
7. **Full Audit** - Everything (costs ~8-10k tokens)

Example: 'Explore CMS and Performance' or 'Focus on the hero component'"
```

## 💰 Token Estimates
- Single area: ~1-2k tokens
- 2-3 areas: ~3-5k tokens
- Full audit: ~8-10k tokens

## Git Worktree Pattern (Optional)
```bash
git worktree add -b feature-explore ../explore-branch
# Each agent works in separate worktree
```

## Execution
```
"I'll spawn 5 parallel agents to explore the Webflow structure:
- Agent 1: Mapping [X pages], [Y symbols], [Z components]
- Agent 2: Analyzing [N collections] with [M total items]
- Agent 3: Documenting [style guide/classes/breakpoints]
- Agent 4: Reviewing [custom code in Slater]
- Agent 5: Checking performance bottlenecks

Estimated token usage: ~8,000"
```

## ⏸️ Pause Checkpoint
If uncertain about scope, ask:
"Should I explore [specific area] in more detail?"

## Output Format
```markdown
### 📊 Exploration Results
- Pages: X total (Y using component Z)
- Symbols: X total (Y instances)
- CMS: X collections, Y items (Z% of 10k limit)
- Custom Code: X scripts, Y total KB
- Performance: LCP Xs, X unoptimized images
- ⚠️ Issues Found: [list critical problems]
```

## Next Step
Run `/wf-plan` with exploration results.