# Prompt Enhancement Techniques

## ⚡ 1. QUICK IMPROVEMENTS

### Specificity Boosters
- ❌ "Write about X" → ✅ "Write a 500-word beginner's guide to X with 3 examples"
- ❌ "Give tips" → ✅ "List 5 actionable tips with examples"
- ❌ "Help with Y" → ✅ "As a Y expert, diagnose this specific issue"
- ❌ "Analyze this" → ✅ "Analyze this data focusing on trends, anomalies, and actionable insights"
- ❌ "Make it better" → ✅ "Improve clarity, add specific examples, and reduce to 200 words"

### Context Injectors
- **WHO:** Define role + target audience → "You are a [role] helping [audience]"
- **WHAT:** Specify exact deliverable → "Create a [format] that [purpose]"
- **WHY:** State purpose and success criteria → "To achieve [goal], success looks like [outcome]"
- **HOW:** Set format, tone, constraints → "Use [tone], include [elements], limit to [scope]"

---

## ✅ 2. ENHANCEMENT CHECKLIST

1. **Role** - Who is the AI?
2. **Task** - What exactly to do?
3. **Context** - What background?
4. **Format** - How to structure?
5. **Constraints** - What limits?
6. **Examples** - What's good output?
7. **Edge Cases** - Handle ambiguity?

---

## 🧠 3. CORE TECHNIQUES

### 🟢 Basic Techniques (Use First)

**Clear Instructions**
- Number your steps
- Use simple, direct language
- Specify output format

**Role Definition**
```
"You are a [specific role] with expertise in [domain]."
```

**Task Clarity**
```
"Your task is to [specific action] for [purpose]."
```

### 🟡 Intermediate Techniques (Add When Needed)

**Chain-of-Thought (CoT)**
```
"Think through this step-by-step:
1. First, analyze [X]
2. Then, consider [Y]
3. Finally, synthesize [Z]
Show your reasoning process."
```

**Structure & Clarity**
- Use delimiters: `"""` for examples, `---` for sections
- Include 1-3 examples when helpful
- Front-load critical information

**Output Specifications**
- "Format as [structure]"
- "Length: [word/item count]"
- "Style: [tone description]"

### 🔴 Advanced Techniques (For Complex Prompts Only)

**Meta-cognition**
- "Before answering, consider what assumptions you're making"
- "Identify any ambiguities in the request"

**Self-validation**
- "After completing, verify your response meets all requirements"
- "Check your work for accuracy and completeness"

**Progressive disclosure**
- "Provide answer in 3 levels: summary, explanation, detailed analysis"

**Divergent/convergent thinking**
- "Generate 5 different approaches, then select and develop the best one"

---

## 📊 4. OUTPUT SPECIFICATIONS

### Format Options
- "Numbered list with explanations"
- "Table with columns [X, Y, Z]"
- "Executive summary + detailed sections"
- "Markdown with headers and bullets"

### Length Guidelines
- Word count: "~200 words"
- Items: "exactly 7"
- Sections: "3 main, 2-3 sub each"
- Read time: "5-minute read"

### Style Options
- "Professional but conversational"
- "Technical yet accessible"
- "Academic with practical examples"