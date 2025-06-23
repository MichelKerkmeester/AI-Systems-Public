# Prompt Enhancement Techniques

**Practical methods and strategies** for improving prompt clarity, specificity, and effectiveness. Organized by complexity level to match your needs and model capabilities.

---

## 🌐 UNIVERSAL MODE (Model-Agnostic)

When model is unknown or for maximum compatibility, use these essentials:

1. **Clear Role:** "You are a [specific expert]"
2. **Explicit Task:** "Your task is to [specific action]"
3. **One Example:** Show desired output format
4. **Simple Format:** Use numbered lists or markdown
5. **No Advanced Features:** Avoid meta-cognition, self-validation

**Universal Template:**
```
You are a [role].
Task: [specific action]
Format: [simple structure]
Example: [show desired output]
```

---

## ⚡ 1. QUICK IMPROVEMENTS

### Specificity Boosters
Transform vague requests into precise instructions:

- ❌ "Write about X" → ✅ "Write a 300-word beginner's guide to X with 3 examples"
- ❌ "Give tips" → ✅ "List 5 actionable tips with 1-2 sentence explanations"
- ❌ "Help with Y" → ✅ "As a Y expert, diagnose this specific issue and suggest solutions"
- ❌ "Analyze this" → ✅ "Analyze this data for trends, anomalies, and actionable insights"
- ❌ "Make it better" → ✅ "Improve clarity, add examples, keep under 300 words"

### Context Injectors
Add essential context using the WHO-WHAT-WHY-HOW framework:

- **WHO:** "You are a [role] helping [audience]"
- **WHAT:** "Create a [format] that [purpose]"
- **WHY:** "To achieve [goal], where success means [outcome]"
- **HOW:** "Use [tone], include [elements], stay within [limits]"

---

## ✅ 2. ENHANCEMENT CHECKLIST

Every enhanced prompt should include:

1. **Role** - Expert identity or perspective
2. **Task** - Specific action with clear verb
3. **Context** - Relevant background information
4. **Format** - Output structure and style
5. **Constraints** - Length, scope, or content limits
6. **Examples** - Sample of desired output
7. **Edge Cases** - How to handle unclear situations

---

## 🧠 3. CORE TECHNIQUES BY COMPLEXITY

### 🟢 Basic Techniques (Always Use)

**Clear Instructions**
- Number sequential steps
- Use action verbs
- Specify deliverables

**Role Definition**
```
"You are a [specific role] with expertise in [domain]."
```

**Task Clarity**
```
"Your task is to [action verb] [specific deliverable] for [purpose]."
```

### 🟡 Intermediate Techniques (When Helpful)

**Chain-of-Thought (CoT)**
```
"Think step-by-step:
1. First, [analyze/identify] [X]
2. Then, [evaluate/consider] [Y]
3. Finally, [conclude/recommend] [Z]
Show your reasoning."
```

**Structure & Formatting**
- Delimiters: `"""` for examples, `---` for sections
- Examples: Include 1-3 relevant samples
- Hierarchy: Use headers and subheaders
- Priority: Front-load critical information

### 🔴 Advanced Techniques (Complex Tasks Only)

**Meta-cognition Triggers**
- "Before starting, identify any assumptions"
- "Consider alternative interpretations"
- "Note confidence levels for each point"

**Self-validation Loops**
- "After completing, verify all requirements are met"
- "Check for internal consistency"
- "Ensure accessibility for target audience"

**Multi-level Output**
- "Provide: 1) Executive summary 2) Detailed analysis 3) Technical appendix"
- "Structure as: Overview → Details → Examples → Edge cases"

---

## 📊 4. OUTPUT SPECIFICATIONS

### Format Templates
- **Lists:** "Numbered list with 1-2 sentence explanations"
- **Tables:** "3-column table: Feature | Benefit | Example"
- **Reports:** "Executive summary + 3 main sections + recommendations"
- **Guides:** "Introduction + step-by-step process + troubleshooting"

### Length Guidelines
- **Optimal:** 300-500 words for comprehensive prompts
- **Brief:** 100-200 words for simple tasks
- **Detailed:** 500-750 words for complex multi-step tasks
- **Sections:** 3-5 main points with 2-3 sub-points each

### Style Calibration
- **Professional:** "Formal tone, industry terminology, evidence-based"
- **Educational:** "Clear explanations, avoid jargon, include examples"
- **Conversational:** "Friendly tone, use 'you', relatable examples"
- **Technical:** "Precise language, include specs, assume expertise"

---

## 🎯 5. COMMON ENHANCEMENT PATTERNS

### From Vague → Specific
1. Add measurable quantities
2. Define scope boundaries
3. Specify format requirements
4. Include success criteria
5. Provide comparison points

### From Simple → Sophisticated
1. Basic task statement
2. Add role expertise
3. Include reasoning steps
4. Add validation criteria
5. Build in edge case handling

### From Broad → Focused
1. Narrow the domain
2. Define target audience
3. Clarify primary objective
4. Set clear constraints
5. Prioritize outcomes