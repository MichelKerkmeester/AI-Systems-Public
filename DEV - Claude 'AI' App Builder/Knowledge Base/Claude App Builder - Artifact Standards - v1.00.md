# Claude App Builder - Artifact Standards

**Essential patterns and standards for building apps in Claude artifacts.**

## 📑 TABLE OF CONTENTS

1. [Key Constraints](#1-key-constraints)
2. [README Standards](#2-readme-standards)
3. [Download & Export Patterns](#3-download--export-patterns)
4. [Clipboard Integration](#4-clipboard-integration)

---

## 1. KEY CONSTRAINTS

### Critical Reminders
- **NO localStorage** - Use React state only
- **NO external APIs** - Only `window.claude.complete`
- **NO server-side code** - Client-side only
- **Pre-compiled Tailwind** - Utility classes only
- **File uploads** - Use `window.fs.readFile(fileName, {encoding})`

---

## 2. README STANDARDS

**Always create as a separate markdown artifact**

### Required Structure

```markdown
# [App Name] - README

## Overview
[Detailed description of the app's purpose and capabilities]

## Features
- ✨ [Feature 1]: [Description]
- ✨ [Feature 2]: [Description]
- 🚀 [Feature 3]: [Description]

## Version History
### v2.0.0 - [Update Name] (2024-01-20)
- 💥 BREAKING: [Breaking change description]
- ✨ Added: [New feature]

### v1.1.0 - [Update Name] (2024-01-15)
- ✨ Added: [New feature]
- 🐛 Fixed: [Bug fix]
- ⚡ Improved: [Performance enhancement]

### v1.0.0 - Initial Release (2024-01-10)
- ✨ [Initial features]

## Usage Guide
### Getting Started
[Step-by-step instructions]

### Advanced Features
[Complex functionality explained]

## Technical Architecture
- **Mode**: $[mode]
- **State Management**: [Approach used]
- **Key Libraries**: [React, Recharts, etc.]
- **MCP Features**: [If any]

## Known Limitations
- [Limitation 1]
- [Limitation 2]

## Troubleshooting
| Issue | Solution |
|-------|----------|
| [Common problem] | [How to fix] |
```

---

## 3. DOWNLOAD & EXPORT PATTERNS

### Text/JSON Download
```javascript
const downloadAsFile = (content, filename, type = 'text/plain') => {
  const blob = new Blob([content], { type });
  const url = URL.createObjectURL(blob);
  const link = document.createElement('a');
  link.href = url;
  link.download = filename;
  link.click();
  URL.revokeObjectURL(url);
};

// Usage
downloadAsFile(JSON.stringify(data, null, 2), 'data.json', 'application/json');
downloadAsFile(csvContent, 'export.csv', 'text/csv');
```

### Canvas/Chart Export
```javascript
const exportChartAsImage = (chartRef, filename = 'chart.png') => {
  // For canvas-based charts
  const canvas = chartRef.current.querySelector('canvas');
  canvas.toBlob(blob => {
    const url = URL.createObjectURL(blob);
    const link = document.createElement('a');
    link.href = url;
    link.download = filename;
    link.click();
    URL.revokeObjectURL(url);
  });
};
```

### CSV Generation
```javascript
const generateCSV = (data, headers) => {
  const csvHeaders = headers.join(',');
  const csvRows = data.map(row => 
    headers.map(header => {
      const value = row[header]?.toString() || '';
      // Escape quotes and wrap in quotes if contains comma
      return value.includes(',') ? `"${value.replace(/"/g, '""')}"` : value;
    }).join(',')
  );
  
  return [csvHeaders, ...csvRows].join('\n');
};
```

---

## 4. CLIPBOARD INTEGRATION

### Copy to Clipboard with Fallback
```javascript
const copyToClipboard = async (text) => {
  try {
    await navigator.clipboard.writeText(text);
    return { success: true };
  } catch (err) {
    // Fallback for older browsers
    const textarea = document.createElement('textarea');
    textarea.value = text;
    textarea.style.position = 'fixed';
    textarea.style.opacity = '0';
    document.body.appendChild(textarea);
    textarea.select();
    
    try {
      document.execCommand('copy');
      return { success: true };
    } catch (err) {
      return { success: false, error: err.message };
    } finally {
      document.body.removeChild(textarea);
    }
  }
};

// With UI feedback
const CopyButton = ({ text }) => {
  const [copied, setCopied] = useState(false);
  
  const handleCopy = async () => {
    const result = await copyToClipboard(text);
    if (result.success) {
      setCopied(true);
      setTimeout(() => setCopied(false), 2000);
    }
  };
  
  return (
    <button onClick={handleCopy}>
      {copied ? '✓ Copied!' : 'Copy'}
    </button>
  );
};
```

### Rich Content Copy
```javascript
const copyRichContent = async (html, plainText) => {
  try {
    const blob = new Blob([html], { type: 'text/html' });
    const richItem = new ClipboardItem({
      'text/html': blob,
      'text/plain': new Blob([plainText], { type: 'text/plain' })
    });
    await navigator.clipboard.write([richItem]);
    return { success: true };
  } catch (err) {
    // Fallback to plain text
    return copyToClipboard(plainText);
  }
};
```

---

*Essential patterns for Claude artifact development. Focus on what's unique to the artifact environment.*