# Dev Ticket Writer - User Guide

## 🚀 What is This?

The Dev Ticket Writer system transforms any request into clear, actionable development tickets. Instead of vague requirements or technical jargon, you get tickets that communicate user value and business outcomes, letting developers focus on HOW to implement.

**Key Benefits:**
- Transform unclear requests into actionable tickets
- Communicate user value and business impact clearly
- Get consistent ticket format across your team
- Focus on WHAT and WHY, not HOW
- Save time with structured templates
- Professional presentation with icons in all modes

**Key Principle:** If a ticket takes more than 2 minutes to read, it's too long.

.

## 📋 Quick Setup in Claude

### Step 1: Create a New Project
1. Go to [claude.ai](https://claude.ai)
2. Click "Projects" in the sidebar
3. Click "Create project"
4. Name it "Dev Ticket Writer"

### Step 2: Add the System Instructions
1. In your project, click "Edit project details"
2. Find the "Custom instructions" section
3. Copy and paste the main system file: `Writer - Dev Tickets - v1.6.md`
4. Save the project

### Step 3: Upload Reference Document
Upload the examples document to your project:
- `Dev Tickets - Examples & Patterns.md` (contains all ticket examples and patterns)

### Step 4: Start Writing Tickets!
Begin any conversation in the project, and Claude will transform your requests into proper dev tickets.

.

## 🧠 Optional Enhancement: Sequential Thinking MCP

### What is Sequential Thinking MCP?
The Sequential Thinking MCP (Model Context Protocol) is a tool that enhances Claude's analytical capabilities by forcing systematic, step-by-step thinking before generating responses. When enabled, the system analyzes your feature request through multiple "thoughts" before writing tickets, resulting in more complete and well-structured tickets.

### Why Use It for Dev Tickets?
- **Better requirement analysis**: System thoroughly analyzes user needs before writing
- **Fewer clarifications needed**: Systematic thinking catches missing details early
- **More complete tickets**: Considers edge cases and dependencies automatically
- **Consistent structure**: Ensures all ticket components are properly addressed
- **Smarter mode selection**: Better analysis of complexity to choose the right ticket mode

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

### How It Works with Dev Tickets
When Sequential Thinking MCP is available, the Dev Ticket Writer automatically:
- Uses it for all ticket creation requests
- Analyzes through 3+ thoughts:
  - Understanding the feature request and user context
  - Identifying missing information or clarifications
  - Planning ticket structure and selecting appropriate mode
- Only bypasses it for simple ticket edits
- Creates more thorough and well-structured tickets

**Note**: The system works perfectly without Sequential Thinking MCP. If it's not installed, you'll see "Sequential Thinking MCP not available, proceeding with standard analysis" and tickets will still be created using the system's built-in intelligence.

.

## 🎯 How to Use

### Basic Usage
Simply describe what you need:
```
We need search filters for our product catalog
```

### Mode Selection
The system has four modes for different complexity levels:

| Mode | Command | Use For |
|------|---------|---------|
| **Quick** | `$q` | Simple, single features |
| **Standard** | `$s` (DEFAULT) | Most features and improvements |
| **Complex** | `$c` | Multi-phase implementations |
| **Epic** | `$e` | Major initiatives with child tickets |

### Mode Examples:
```
$q add logout button to header

$s implement user profile editing with avatar upload

$c rebuild search system with filters, personalization, and analytics

$e create customer self-service portal
```

.

## ✅ Output Format

### Every Ticket Includes:
1. **Always in an artifact** (for easy copying)
2. **User Value statement** (why it matters)
3. **Business Goal** (measurable impact)
4. **Requirements** (outcome-focused, not technical)
5. **Success Criteria** (measurable checkboxes)
6. **Design links** (when applicable)
7. **Dependencies** (related tickets)
8. **Icons throughout** (for visual hierarchy in all modes)

### Example Output Structure:
```markdown
### ❖ Search Filters

**User Value:** Find relevant products faster

**Business Goal:** Reduce search abandonment by 30%

---

## ◇ Requirements
- Filter by category, price, availability
- Results update instantly
- Mobile-responsive design

## → Design
- [Figma - Search Filters](link)

## ✓ Success Criteria
- [ ] Filters work on all devices
- [ ] Results update in <300ms
- [ ] 30% reduction in abandonment

## ⊗ Dependencies
- Requires: Search API v2 (#1234)
```

### Icon Reference:
- **❖** Feature titles
- **◇** Requirements sections
- **→** Design sections
- **✓** Success criteria
- **⊗** Dependencies
- **⚠️** Risks/warnings
- **⌘** About/context sections

.

## 🆘 Troubleshooting

### "It's providing technical solutions"
- Make sure you're in the Dev Ticket Writer project
- The system should focus on WHAT not HOW
- Check that custom instructions are saved properly

### "The ticket is too long/detailed"
- Use `$q` mode for simpler tickets
- Default `$s` mode balances completeness and brevity
- Remember: 2-minute read rule

### "I need multiple related tickets"
- Use `$e` epic mode for major initiatives
- Ask to split complex features into phases
- Each ticket should be one deployable unit

### "Missing design links"
- The system will note "Needs: Design mockups"
- Tickets can proceed with placeholder for designs
- Add actual links when available

### "Icons aren't showing in tickets"
- Icons should appear in ALL modes (Quick, Standard, Complex, Epic)
- Every major section should have an icon
- Check that you're using the latest version (v1.6)

### "Sequential Thinking MCP not working"
- Check if it shows in the 🔌 tools menu
- Verify your config file syntax is correct
- Restart Claude Desktop after configuration changes
- System works fine without it (just notes it's unavailable)