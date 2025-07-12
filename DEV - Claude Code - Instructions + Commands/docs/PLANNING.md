# PLANNING.md - Anobel.nl Project Strategy

## 🎯 Project Overview
**Project**: Anobel.nl Website Enhancement
**Type**: Webflow-based website with custom JavaScript/CSS enhancements
**Status**: Active Development

## 📋 Project Context
- **Platform**: Webflow + Custom Code
- **Code Hosting**: Slater (for deployment)
- **Development Environment**: Local IDE
- **Version Control**: Git

## 🏗️ Architecture Overview
```
anobel.nl/
├── .claude/           # Claude Code configuration
├── docs/
│   ├── production/    # Active project documentation
│   └── templates/     # Reference templates
├── src/               # Source code (if applicable)
└── CLAUDE.md          # AI assistant instructions
```

## 🎯 Current Goals
1. Enhance Webflow site with custom JavaScript functionality
2. Maintain clean, performant, accessible code
3. Follow Webflow best practices and constraints
4. Document all custom implementations

## ⚡ Technical Constraints
- **NO DOM Manipulation**: Work with existing Webflow structure
- **REM Units Only**: No pixel values in CSS
- **Progressive Enhancement**: Site must work without JS
- **Performance Budget**: < 50KB JS, 60 FPS animations

## 📚 Key Resources
- **Webflow Designer**: Visual structure (read-only)
- **Slater**: Code deployment platform
- **Motion.dev**: Default animation library
- **Custom Commands**: /workflow, /check, /mcp, /validate, /pr

## 🔄 Development Workflow
1. **Explore** existing Webflow structure
2. **Plan** enhancement architecture
3. **Code** with progressive enhancement
4. **Validate** using /check command
5. **Deploy** via Slater

## 📝 Notes
- Always check for existing Webflow interactions before adding JS
- Use data attributes for JavaScript hooks
- Follow the established MCP tool decision tree
- Document all data attributes required for functionality

---
*Last Updated: July 12, 2025*