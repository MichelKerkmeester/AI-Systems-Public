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
6. **Code Base** - IDE scripts structure, architecture patterns
7. **Specific Component** - Deep dive on one element
8. **Full Audit** - Everything (costs ~8-10k tokens)

Example: 'Explore CMS and Code Base' or 'Focus on the hero component'"
```

## 💰 Token Estimates
- Single area: ~1-2k tokens
- 2-3 areas: ~3-5k tokens
- Code Base analysis: ~2-3k tokens
- Full audit: ~10-12k tokens

## Targeted Exploration

Based on your selection, I'll spawn only needed agents:

### For "Structure" Exploration
```
"Spawning Structure Agent to analyze:
- All pages and their hierarchy
- Symbol usage and instances
- Component relationships
- Interaction patterns"
```

### For "CMS" Exploration
```
"Spawning CMS Agent to analyze:
- Collections: [names and item counts]
- Field types and references
- Current usage: X/10,000 items (Y%)
- Multi-reference relationships"
```

### For "Performance" Exploration
```
"Spawning Performance Agent to check:
- Image optimization status
- Font loading strategy
- Script impact on load time
- Current Core Web Vitals"
```

### For "Code Base" Exploration
```
"Spawning Code Architecture Agent to analyze:
- File structure and organization
- Module dependencies and imports
- Reusable utilities and helpers
- Code patterns and conventions
- Integration points with Slater"
```

### For "Specific Component"
```
"Which component should I analyze in detail?
I'll check its usage across all pages, variations, 
and performance impact."
```

## Parallel Execution (When Multiple Selected)
```
"You selected: Code Base + Webflow Structure

Spawning 2 parallel agents:
- Agent 1: Analyzing IDE codebase and architecture
- Agent 2: Mapping Webflow pages and components

Estimated tokens: ~4,000"
```

Example for mixed exploration:
```
"You selected: CMS + Code Base + Performance

Spawning 3 parallel agents:
- Agent 1: Analyzing CMS structure and usage
- Agent 2: Reviewing code architecture in IDE
- Agent 3: Running performance audit

Estimated tokens: ~6,000"
```

## Git Worktree Pattern (For Full Audit)
```bash
git worktree add -b feature-explore ../explore-branch
# Each agent works in separate worktree
```

## 📊 Output Format (Adapts to Selection)

### Minimal (1-2 areas)
```markdown
### 🔍 Targeted Exploration: [Areas]
[Specific findings for selected areas only]
```

### Comprehensive (3+ areas or Full Audit)
```markdown
### 📊 Exploration Results
- Pages: X total (Y using component Z)
- Symbols: X total (Y instances)
- CMS: X collections, Y items (Z% of 10k limit)
- Custom Code: X scripts, Y total KB
- Performance: LCP Xs, X unoptimized images
- ⚠️ Issues Found: [list critical problems]
```

## Smart Recommendations
Based on exploration, I'll suggest:
- If near CMS limits → "Consider archiving old items"
- If performance issues → "Run `/wf-validate` for detailed metrics"
- If complex structure → "Create visual sitemap"

## Next Step
- For targeted exploration → Implement findings
- For full audit → Run `/wf-plan` with complete results
- If issues found → Run `/wf-risk` for mitigation strategies