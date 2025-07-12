# 🤖 Claude App Builder v2.0

A streamlined system that transforms Claude into an elite app architect, building functional web applications and AI demos directly in Claude artifacts.

## Overview

The Claude App Builder enables rapid development of web applications within Claude's artifact environment. With three focused modes ($app, $ai, $data) and mandatory code reasoning optimization, it delivers production-ready applications that work immediately.

 .

## ✨ Key Features

- **3 Specialized Modes**: $app (general apps), $ai (AI-powered interfaces), $data (dashboards & visualization)
- **MCP Integration**: Optional enhancements via $search, $docs, $ui, and $magic shortcuts
- **Fluid Responsive Design**: Smooth scaling using CSS clamp() formulas
- **Code Reasoning**: Mandatory optimization step for thoughtful architecture
- **Visual Pattern Libraries**: Reference UI patterns for professional designs
- **Zero External Dependencies**: Everything works within artifact constraints
- **Comprehensive Documentation**: Each app includes detailed README

.

## 🚀 Quick Setup

### Step 1: Create a Claude Project
1. Go to claude.ai
2. Click "Projects" in sidebar
3. Click "Create project"
4. Name it "Claude App Builder v2"

### Step 2: Add System Instructions
1. In your project, click "Edit project details"
2. Find "Custom instructions" section
3. Copy and paste: `Claude App Builder - v2.0 (Streamlined).md`
4. Save the project

### Step 3: Upload Supporting Documents
Add these to your project's knowledge base:
- `Claude App Builder - Artifact Standards - v1.01.md`
- `Claude App Builder - Fluid Responsive Guide - v1.01.md`
- `Claude App Builder - Visual Pattern Libraries - v1.00.md`

### Step 4: Enable MCPs (Optional)
Available MCP shortcuts for enhanced features:
- `$search` - Web search integration
- `$docs` - Documentation access
- `$ui` - Shadcn UI components
- `$magic` - Animation effects (only when explicitly requested)

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

## 📚 Documentation

Each app includes:
- Comprehensive README with version history
- Usage instructions and examples
- Technical architecture details
- Known limitations and troubleshooting

## 🔧 Constraints

- **No localStorage**: Use React state
- **No external APIs**: Except window.claude.complete
- **Client-side only**: No server functionality
- **Static Tailwind**: Pre-compiled utilities only

---

*Build complete, functional web applications that work immediately. Focus on user experience and visual quality.*