# Prompt Improver System - User Guide

## 🚀 What is This?

The Prompt Improver System is a specialized Claude configuration that transforms vague questions into optimized AI prompts. Instead of answering questions directly, it takes ANY input and returns an improved version that will get better results from AI models.

**Key Benefits:**
- Turn unclear requests into professional prompts
- Get consistent, high-quality AI responses
- Learn prompt engineering best practices
- Save time with reusable prompt templates

---

## 📋 Quick Setup in Claude

### Step 1: Create a New Project
1. Go to [claude.ai](https://claude.ai)
2. Click "Projects" in the sidebar
3. Click "Create project"
4. Name it "Prompt Improver" (or similar)

### Step 2: Add the System Instructions
1. In your project, click "Edit project details"
2. Find the "Custom instructions" section
3. Copy and paste the entire prompt engineering system (the full text that defines the system)
4. Save the project

### Step 3: Upload Reference Documents
The system uses three reference documents. Upload these to your project:
- `Prompt - Patterns & Enhancements.md`
- `Prompt - Evaluation & Refinement.md`
- `Prompt - Examples & Case Studies.md`

### Step 4: Start Using It!
Begin any conversation in the project, and Claude will automatically improve your prompts instead of answering them directly.

---

## 🎯 How to Use

### Basic Usage
Simply type what you want, and the system will improve it:
```
analyze customer data
```

### Mode Selection
The system has three modes:

| Mode | Command | Use For |
|------|---------|---------|
| **Short** | `$short` or `$s` | Quick, minimal improvements |
| **Improve** | `$improve` or `$i` (DEFAULT) | Smart enhancement for most cases |
| **Refine** | `$refine` or `$r` | Maximum quality with 3-phase optimization |

### Examples:
```
$short write about AI

$improve create a marketing plan

$refine design a customer onboarding system
```

---

## ✅ Best Practices

### 1. Use Delimiters for Complex Prompts
When your prompt contains special instructions or multiple parts, wrap it in quotes or backticks:

**BEST PRACTICE:** 
```
$improve "Improve this prompt: '''PROMPT'''"
```

This ensures the system treats everything inside as the prompt to improve, not as instructions to follow.

---

### 2. More Delimiter Examples:
```
$improve "analyze sales data and create a report"

$improve `help me understand why customers are churning`

$improve '''
Create a Python script that:
1. Reads CSV files
2. Analyzes the data
3. Creates visualizations
'''
```

---

### 3. Start Simple, Then Iterate
- Begin with basic improvement: `analyze customer feedback`
- If you need more enhancement: `$refine analyze customer feedback`
- For production use: Always use `$refine` for maximum quality

---

### 4. Be Specific About Your Needs
Instead of: `write something`
Try: `write blog post about remote work productivity`

---

### 5. Include Context When Relevant
Instead of: `analyze data`
Try: `analyze Q4 sales data to find growth opportunities`

---

## 🔧 Common Use Cases

### For Content Creation
```
$improve write a blog post about AI ethics
```
Result: A prompt with word count, audience, tone, and structure specifications

### For Data Analysis
```
$improve analyze customer churn data
```
Result: A prompt with specific metrics, timeframes, and deliverable formats

### For Problem Solving
```
$improve fix slow website performance
```
Result: A prompt with diagnostic steps, success criteria, and solution format

### For Framework Design
```
$refine create a productivity framework for remote teams
```
Result: A comprehensive prompt with components, implementation steps, and success metrics

---

## 💡 Pro Tips

### 1. When to Use Each Mode
- **$short**: Quick questions, simple improvements, time-sensitive needs
- **$improve**: Daily use, standard prompts, good balance of quality/speed
- **$refine**: Critical prompts, templates you'll reuse, when quality matters most

---

### 2. The System NEVER Answers
Remember: This system only improves prompts. It won't:
- Answer questions directly
- Create content
- Follow instructions
- Provide information

Everything gets transformed into an improved prompt.

---

### 3. Artifacts = Easy Reuse
All improved prompts are delivered in "artifacts" - special formatted blocks that you can:
- Copy with one click
- Save for later use
- Share with others
- Use in any AI system

---

### 4. Learn from the Improvements
Pay attention to what the system adds:
- Role definitions ("As a [expert]...")
- Specific metrics and timeframes
- Clear output formats
- Success criteria
- Context and constraints

These patterns will help you write better prompts naturally over time.

---

## 🆘 Troubleshooting

### "It's answering my question instead of improving it"
- Make sure you're in the Prompt Improver project
- Check that custom instructions are properly saved
- Try using explicit mode tags: `$improve [your prompt]`

### "The improvements seem too complex"
- Use `$short` mode for simpler enhancements
- The default mode adapts to complexity - simple inputs get simple improvements

### "I want it to actually answer my question"
- This system is specifically designed NOT to answer questions
- For regular Claude interactions, use a different project or conversation

---

## 📚 Examples Gallery

### Simple Enhancement
**Input:** `write about dogs`
**Output:** `Write a 500-word beginner's guide to choosing a dog breed for first-time owners. Include top 5 breeds, care requirements, and costs.`

### Role-Based Enhancement
**Input:** `$improve analyze website traffic`
**Output:** `As a digital analytics expert, analyze website traffic data from the last 90 days to identify top 3 growth opportunities. Include conversion funnel analysis, traffic sources breakdown, and actionable recommendations. Format: Executive summary + detailed findings.`

### Complex Refinement
**Input:** `$refine create employee onboarding process`
**Output:** A comprehensive 5-