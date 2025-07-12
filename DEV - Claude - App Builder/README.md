# 🤖 Claude App Builder v1.3.1

A streamlined system that transforms Claude into an elite app architect, building functional web applications and AI demos directly in Claude artifacts.

## Overview

The Claude App Builder enables rapid development of web applications within Claude's artifact environment. With three focused modes ($app, $ai, $data) and mandatory sequential thinking optimization, it delivers production-ready applications that work immediately.

 .

## ✨ Key Features

- **3 Specialized Modes**: $app (general apps), $ai (AI-powered interfaces), $data (dashboards & visualization)
- **MCP Integration**: Optional enhancements via $search, $docs, $ui, and $magic shortcuts
- **Fluid Responsive Design**: Smooth scaling using CSS clamp() formulas
- **Sequential Thinking**: Mandatory optimization step for thoughtful architecture
- **Visual Pattern Libraries**: Reference UI patterns for professional designs
- **Zero External Dependencies**: Everything works within artifact constraints
- **Comprehensive Documentation**: Each app includes detailed README

.

## 🚀 Quick Setup

### Step 1: Create a Claude Project
1. Go to claude.ai
2. Click "Projects" in sidebar
3. Click "Create project"
4. Name it "Claude App Builder v1.3"

### Step 2: Add System Instructions
1. In your project, click "Edit project details"
2. Find "Custom instructions" section
3. Copy and paste: `DEV - Claude App Builder - v1.3.0.md`
4. Save the project

### Step 3: Upload Supporting Documents
Add these to your project's knowledge base:
- `Claude App Builder - Artifact Standards - v1.0.1.md`
- `Claude App Builder - Fluid Responsive Guide - v1.0.1.md`
- `Claude App Builder - Visual Pattern Libraries - v1.0.0.md`

### Step 4: Enable MCP Features
Available MCP shortcuts for enhanced features:
- `$search` - Web search integration (requires Tavily or Brave Search MCP)
- `$docs` - Documentation access (requires Context7 MCP)
- `$ui` - Shadcn UI components (built-in, no MCP needed)
- `$magic` - Animation effects (built-in, only when explicitly requested)

### Step 5: Start Building
Simply describe what you want with the appropriate mode:
```
Build a $app todo list manager
Create an $ai chatbot assistant
Make a $data sales dashboard
```

.

## 📋 System Modes

| Mode | Purpose | Use Cases |
|------|---------|-----------|
| **$app** | General web applications | Tools, utilities, CRUD apps |
| **$ai** | AI-powered interfaces | Chatbots, assistants, multi-agent systems |
| **$data** | Data visualization | Dashboards, analytics, CSV analysis |

.

## 🛠️ Technical Stack

### Pre-loaded Libraries
- React 18, Tailwind CSS (utilities only)
- Recharts, Lodash, Papaparse, XLSX
- Three.js r128, D3.js, Chart.js
- TensorFlow.js, Tone.js

### Claude-Specific APIs
- `window.claude.complete()` - AI completions
- `window.fs.readFile()` - File reading
- No localStorage - React state only
- Client-side only - No server capabilities

.

## 🔧 Constraints

- **No localStorage**: Use React state
- **No external APIs**: Except window.claude.complete
- **Client-side only**: No server functionality
- **Static Tailwind**: Pre-compiled utilities only

## 📚 Documentation

Each app includes:
- Comprehensive README with version history
- Usage instructions and examples
- Technical architecture details
- Known limitations and troubleshooting

.

## 📦 MCP Installation Guide

MCPs (Model Context Protocol) extend Claude's capabilities. Here's how to install the essential ones:

### Sequential Thinking Tool (Required)
1. In Claude Desktop, go to Settings → Developer
2. Click "Add MCP Server"
3. Add the following configuration:
```json
{
  "sequential-thinking": {
    "command": "npx",
    "args": ["-y", "@modelcontextprotocol/server-sequential-thinking"]
  }
}
```

### Web Search MCPs (for $search)
Choose one or both:

**Tavily Search:**
```json
{
  "tavily": {
    "command": "npx",
    "args": ["-y", "@modelcontextprotocol/server-tavily"],
    "env": {
      "TAVILY_API_KEY": "your-api-key-here"
    }
  }
}
```

**Brave Search:**
```json
{
  "brave-search": {
    "command": "npx",
    "args": ["-y", "@modelcontextprotocol/server-brave-search"],
    "env": {
      "BRAVE_API_KEY": "your-api-key-here"
    }
  }
}
```

### UI Component MCPs (for $ui and $magic)

**Shadcn UI (for $ui):**
```json
{
  "shadcn": {
    "command": "npx",
    "args": ["-y", "@modelcontextprotocol/server-shadcn"]
  }
}
```

**Magic UI (for $magic):**
```json
{
  "magic-ui": {
    "command": "npx",
    "args": ["-y", "@modelcontextprotocol/server-magic-ui"]
  }
}
```

### Documentation Access (for $docs)
**Context7:**
```json
{
  "context7": {
    "command": "npx",
    "args": ["-y", "@context7/mcp-server"]
  }
}
```

### Notes:
- Replace `your-api-key-here` with actual API keys from the respective services
- Restart Claude Desktop after adding MCPs
- The `$ui` and `$magic` shortcuts don't require separate MCP installation
- Sequential Thinking is essential for the app builder's optimization step

---

*Build complete, functional web applications that work immediately. Focus on user experience and visual quality.*