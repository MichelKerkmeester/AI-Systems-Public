# Prompt Improver System - User Guide

## 🚀 What is This?

The Prompt Improver System is a specialized Claude configuration that transforms vague questions into optimized AI prompts. Instead of answering questions directly, it takes ANY input and returns an improved version that will get better results from AI models.

**Key Benefits:**
- Turn unclear requests into professional prompts
- Get consistent, high-quality AI responses
- Learn prompt engineering best practices
- Save time with reusable prompt templates

.

## 📋 Quick Setup in Claude

### Step 1: Create a New Project
1. Go to [claude.ai](https://claude.ai)
2. Click "Projects" in the sidebar
3. Click "Create project"
4. Name it "Prompt Improver" (or similar)

### Step 2: Add the System Instructions
1. In your project, click "Edit project details"
2. Find the "Custom instructions" section
3. Copy and paste the main system file: `Writer - Prompt Improver - v2.8.md`
4. Save the project

### Step 3: Upload Reference Documents
The system uses three reference documents. Upload these to your project:
- `Prompt - Patterns & Enhancements.md`
- `Prompt - Evaluation & Refinement.md`
- `Prompt - Examples & Case Studies.md`

### Step 4: Start Using It!
Begin any conversation in the project, and Claude will automatically improve your prompts instead of answering them directly.

.

## 🧠 Optional Enhancement: Sequential Thinking MCP

### What is Sequential Thinking MCP?
The Sequential Thinking MCP (Model Context Protocol) is a tool that enhances Claude's analytical capabilities by forcing systematic, step-by-step thinking before generating responses. When enabled, the system analyzes prompts through multiple "thoughts" before improving them, resulting in more nuanced and effective enhancements.

### Why Use It for Prompt Improvement?
- **Deeper pattern analysis**: System identifies prompt weaknesses more systematically
- **Better enhancement selection**: Chooses the most appropriate improvement techniques
- **Smarter complexity matching**: Better adapts improvements to prompt complexity
- **More creative approaches**: Sequential analysis often reveals unique enhancement angles
- **Consistent quality**: Ensures no aspect of prompt improvement is overlooked

### How to Install Sequential Thinking MCP

**Prerequisites:**
- Claude Desktop app installed
- Basic familiarity with editing configuration files

**Installation Steps:**

1. **Locate your Claude Desktop configuration:**
   - **macOS**: `~/Library/Application Support/Claude/claude_desktop_config.json`
   - **Windows**: `%APPDATA%\Claude\claude_desktop_config.json`

2. **Edit the configuration file** to add Sequential Thinking MCP:
```json
{
  "mcpServers": {
    "sequential-thinking": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-sequential-thinking"
      ]
    }
  }
}
```

3. **If you already have other MCP servers**, add Sequential Thinking to the existing list:
```json
{
  "mcpServers": {
    "filesystem": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-filesystem", "/path/to/allowed/files"]
    },
    "sequential-thinking": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-sequential-thinking"
      ]
    }
  }
}
```

4. **Save the file and restart Claude Desktop**

5. **Verify installation** by starting a new chat and looking for the 🔌 icon, which should show "sequential-thinking" as an available tool

### How It Works with Prompt Improver
When Sequential Thinking MCP is available, the Prompt Improver automatically:
- Uses it for all prompt improvement requests
- Analyzes through 3+ thoughts:
  - Understanding user intent and prompt type
  - Identifying weaknesses and enhancement opportunities
  - Planning improvement approach and pattern selection
- Only bypasses it for simple prompt edits
- Creates more sophisticated and effective improvements

**Note**: The system works perfectly without Sequential Thinking MCP. If it's not installed, you'll see "Sequential Thinking MCP not available, proceeding with standard analysis" and prompts will still be improved using the system's built-in intelligence.

.

## 🎯 How to Use

### Basic Usage
Simply type what you want, and the system will improve it:
```
analyze customer data
```

### Mode Selection
The system has four modes:

| Mode | Command | Use For |
|------|---------|---------|
| **Short** | `$short` or `$s` | Quick, minimal improvements |
| **Improve** | `$improve` or `$i` (DEFAULT) | Smart enhancement for most cases |
| **Refine** | `$refine` or `$r` | Maximum quality with 3-phase optimization |
| **JSON** | `$json` or `$j` | API-ready structured format |

.

## ✅ Best Practices

### 1. Use Delimiters for Complex Prompts
When your prompt contains special instructions or multiple parts, wrap it in quotes or backticks:

**BEST PRACTICE:** 
```
$improve "Improve this prompt: '''PROMPT'''"
```

This ensures the system treats everything inside as the prompt to improve, not as instructions to follow.

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

### 3. Start Simple, Then Iterate
- Begin with basic improvement: `analyze customer feedback`
- If you need more enhancement: `$refine analyze customer feedback`
- For production use: Always use `$refine` for maximum quality

### 4. Be Specific About Your Needs
Instead of: `write something`
Try: `write blog post about remote work productivity`

### 5. Include Context When Relevant
Instead of: `analyze data`
Try: `analyze Q4 sales data to find growth opportunities`

.

## 💡 Pro Tips

### 1. When to Use Each Mode
- **$short**: Quick questions, simple improvements, time-sensitive needs
- **$improve**: Daily use, standard prompts, good balance of quality/speed
- **$refine**: Critical prompts, templates you'll reuse, when quality matters most
- **$json**: API integrations, programmatic use, structured data needs

### 2. The System NEVER Answers
Remember: This system only improves prompts. It won't:
- Answer questions directly
- Create content
- Follow instructions
- Provide information

Everything gets transformed into an improved prompt.

### 3. Artifacts = Easy Reuse
All improved prompts are delivered in "artifacts" - special formatted blocks that you can:
- Copy with one click
- Save for later use
- Share with others
- Use in any AI system

### 4. Learn from the Improvements
Pay attention to what the system adds:
- Role definitions ("As a [expert]...")
- Specific metrics and timeframes
- Clear output formats
- Success criteria
- Context and constraints

These patterns will help you write better prompts naturally over time.

### 5. JSON Mode for Developers
The `$json` mode is perfect for:
- Building AI-powered applications
- Creating reusable prompt templates
- Integrating with APIs
- Storing prompts in databases
- Version control systems

Example JSON structure:
```json
{
  "task": "You are a customer support specialist...",
  "taskRules": [
    "Always maintain professional tone",
    "Respond within 3 sentences"
  ],
  "parameters": {
    "temperature": 0.7,
    "max_tokens": 150
  }
}
```

.

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

### "JSON output isn't valid"
- The JSON mode creates valid, structured JSON
- Check for any manual edits that might have broken the format
- The JSON directly mirrors the improved prompt structure

### "Sequential Thinking MCP not working"
- Check if it shows in the 🔌 tools menu
- Verify your config file syntax is correct
- Restart Claude Desktop after configuration changes
- System works fine without it (just notes it's unavailable)