# Prompt Patterns Reference

**Reusable templates and structural frameworks** for crafting effective prompts across common use cases. Each pattern provides a proven structure that can be customized with specific details while maintaining optimal prompt architecture.

---

## 🚀 1. QUICK TEMPLATES

**Analysis:** "As a [expert], analyze [topic] focusing on [aspect]. Provide [format] with [specifics]."

**Creation:** "Create [thing] for [audience] that [purpose]. Include [must-haves], avoid [exclusions]."

**Solution:** "Solve [problem] given [constraints]. Think step-by-step, then provide [deliverable]."

---

## 📐 2. POWER PATTERNS

### Expert Analysis Pattern
**Best for:** Data interpretation, research evaluation, strategic assessment

```
You are a [specific expert role] with expertise in [domain].
Analyze [subject] considering:
1. [Critical factor 1]
2. [Critical factor 2]
3. [Critical factor 3]

Focus on [priority].
Assume [audience knowledge level].
Format: [structure with examples]
If uncertain about [X], state assumptions clearly.
```

**Example Transformation:**
- **Before:** "Analyze this data"  
- **After:** "You are a data scientist specializing in user behavior. Analyze this e-commerce conversion funnel data to identify the biggest drop-off point. Provide 3 actionable recommendations to improve conversion, backed by specific metrics. Format as executive summary with supporting visualizations."

---

### Structured Creation Pattern
**Best for:** Content generation, documentation, creative deliverables

```
Create [specific deliverable] for [target audience].
Requirements:
- Length: [exact count/range]
- Style: [tone with example]
- Must include: [elements]
- Must avoid: [exclusions]
- Success looks like: [concrete example]

Think step-by-step, then produce the final output.
```

**Example Transformation:**
- **Before:** "Help with social media"  
- **After:** "You are a social media strategist for B2B SaaS. Create a 30-day LinkedIn content calendar for our project management tool. Target: IT managers at mid-size companies. Include 20 posts mixing thought leadership (40%), product education (30%), and industry insights (30%). Provide hooks and CTAs."

---

### Problem-Solving Pattern
**Best for:** Troubleshooting, optimization, strategic solutions

```
Help solve: [specific problem]
Context: [relevant background]
Constraints: [hard limits]
Resources: [available tools/data]
Success criteria: [measurable outcome]

Approach:
1. Diagnose root cause
2. Generate 3 solutions
3. Evaluate trade-offs
4. Recommend best option with rationale
```

**Example Transformation:**
- **Before:** "Make this better"  
- **After:** "You are a UX researcher. Review this customer onboarding flow and identify 3 friction points causing drop-offs. For each friction point, provide: 1) Data/evidence of the issue, 2) User psychology behind it, 3) Specific design solution. Prioritize by impact."

---

## 💡 3. PATTERN COMBINATIONS

For complex requests, combine patterns strategically:

- **Analysis + Creation:** First analyze situation, then create solution
- **Problem + Creation:** Diagnose issue, then build fix
- **Analysis + Problem:** Deep dive into data, then solve identified issues

**Combined Example:**
```
You are a [role]. 
First, analyze [current state] focusing on [metrics].
Then, create [solution] that addresses the top 3 issues.
Requirements: [specs]
Success looks like: [outcome]
```

---

## ⚡ 4. PATTERN SELECTION GUIDE

- **Need analysis?** → Expert Analysis Pattern
- **Need content?** → Structured Creation Pattern  
- **Need solution?** → Problem-Solving Pattern
- **Not sure?** → Try Creation first