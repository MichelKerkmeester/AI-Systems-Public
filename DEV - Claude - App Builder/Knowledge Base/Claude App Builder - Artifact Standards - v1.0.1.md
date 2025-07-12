# Claude App Builder - Artifact Standards v1.02

**Essential patterns and standards for building apps in Claude artifacts.**

## 1. 🔑 KEY CONSTRAINTS

### ⚠️ Critical Reminders
- **NO localStorage** - Use React state only
- **NO external APIs** - Only `window.claude.complete`
- **NO server-side code** - Client-side only
- **Pre-compiled Tailwind** - Utility classes only
- **File uploads** - Use `window.fs.readFile(fileName, {encoding})` - only works with files uploaded to current conversation

---

## 2. 📝 README STANDARDS

**Always create as a separate markdown artifact**

### 📄 Required Structure

```markdown
# [App Name] - README

## Overview
[Detailed description of the app's purpose and capabilities]

## Features
- ✨ [Feature 1]: [Description]
- ✨ [Feature 2]: [Description]
- 🚀 [Feature 3]: [Description]

## Version History
### v2.0.0 - [Update Name] (YYYY-MM-DD)
- 💥 BREAKING: [Breaking change description]
- ✨ Added: [New feature]

### v1.1.0 - [Update Name] (YYYY-MM-DD)
- ✨ Added: [New feature]
- 🐛 Fixed: [Bug fix]
- ⚡ Improved: [Performance enhancement]

### v1.0.0 - Initial Release (YYYY-MM-DD)
- ✨ [Initial features]

## Usage Guide
### Getting Started
[Step-by-step instructions]

### Advanced Features
[Complex functionality explained]

## Technical Architecture
- **Mode**: $[mode]
- **State Management**: [Approach used]
- **Key Libraries**: [React, recharts, etc.]
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

## 3. 🚨 ERROR HANDLING PATTERNS

### 🔄 Claude API Retry with Exponential Backoff
```javascript
const callClaudeWithRetry = async (prompt, maxRetries = 3) => {
  for (let i = 0; i < maxRetries; i++) {
    try {
      const response = await window.claude.complete(prompt);
      // Always parse safely
      try {
        return JSON.parse(response);
      } catch {
        return { text: response }; // Fallback for non-JSON
      }
    } catch (error) {
      if (i === maxRetries - 1) throw error;
      // Exponential backoff: 1s, 2s, 4s
      await new Promise(r => setTimeout(r, 1000 * Math.pow(2, i)));
    }
  }
};
```

### 🎯 User-Friendly Error Display
```javascript
const ErrorDisplay = ({ error, retry }) => (
  <div className="bg-red-50 border border-red-200 rounded-lg p-4">
    <h3 className="text-red-800 font-semibold mb-2">
      Something went wrong
    </h3>
    <p className="text-red-600 text-sm mb-3">
      {error.message || 'An unexpected error occurred'}
    </p>
    {retry && (
      <button 
        onClick={retry}
        className="px-4 py-2 bg-red-600 text-white rounded hover:bg-red-700"
      >
        Try Again
      </button>
    )}
  </div>
);
```

---

## 4. 💾 DOWNLOAD & EXPORT PATTERNS

### 📄 Text/JSON Download
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

### 🖼️ Canvas/Chart Export
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

### 📊 CSV Generation
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

## 5. 📋 CLIPBOARD INTEGRATION

### 📋 Copy to Clipboard with Fallback
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
    <button 
      onClick={handleCopy}
      className="px-3 py-1 bg-gray-100 hover:bg-gray-200 rounded transition-colors"
    >
      {copied ? '✓ Copied!' : 'Copy'}
    </button>
  );
};
```

### 🎨 Rich Content Copy
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

## 6. ⏳ LOADING STATES

### 💀 Skeleton Loader Component
```javascript
const SkeletonLoader = ({ width = "100%", height = "1rem", className = "" }) => (
  <div 
    className={`bg-gray-200 animate-pulse rounded ${className}`}
    style={{ width, height }}
  />
);

// Usage in lists
const LoadingList = () => (
  <div className="space-y-3">
    {[...Array(5)].map((_, i) => (
      <div key={i} className="flex items-center gap-3">
        <SkeletonLoader width="3rem" height="3rem" className="rounded-full" />
        <div className="flex-1">
          <SkeletonLoader height="1.25rem" className="mb-2" />
          <SkeletonLoader width="60%" />
        </div>
      </div>
    ))}
  </div>
);
```

### 📊 Progress Indicator
```javascript
const ProgressBar = ({ progress, label }) => (
  <div className="w-full">
    {label && (
      <div className="flex justify-between text-sm text-gray-600 mb-1">
        <span>{label}</span>
        <span>{Math.round(progress)}%</span>
      </div>
    )}
    <div className="w-full bg-gray-200 rounded-full h-2">
      <div 
        className="bg-blue-500 h-2 rounded-full transition-all duration-300"
        style={{ width: `${progress}%` }}
      />
    </div>
  </div>
);
```

---

## 7. 💿 STATE PERSISTENCE PATTERNS

### 🗄️ Session-Only State Management
```javascript
// Custom hook for session persistence (no localStorage)
const useSessionState = (key, initialValue) => {
  const [state, setState] = useState(() => {
    // Could retrieve from parent component or context
    return initialValue;
  });
  
  // Optional: Notify parent component of changes
  const updateState = useCallback((newValue) => {
    setState(newValue);
    // Could emit event or call callback here
  }, []);
  
  return [state, updateState];
};
```

### ↩️ State Recovery Pattern
```javascript
const useRecoverableState = (initialState) => {
  const [state, setState] = useState(initialState);
  const [history, setHistory] = useState([initialState]);
  const [historyIndex, setHistoryIndex] = useState(0);
  
  const updateState = (newState) => {
    const newHistory = history.slice(0, historyIndex + 1);
    newHistory.push(newState);
    setHistory(newHistory);
    setHistoryIndex(newHistory.length - 1);
    setState(newState);
  };
  
  const undo = () => {
    if (historyIndex > 0) {
      setHistoryIndex(historyIndex - 1);
      setState(history[historyIndex - 1]);
    }
  };
  
  const redo = () => {
    if (historyIndex < history.length - 1) {
      setHistoryIndex(historyIndex + 1);
      setState(history[historyIndex + 1]);
    }
  };
  
  return { state, updateState, undo, redo, canUndo: historyIndex > 0, canRedo: historyIndex < history.length - 1 };
};
```

---

## 8. 🔌 MCP COMPONENT INTEGRATION

### 🔧 Fetching Components via MCP
```javascript
// Pattern for including Shadcn/Magic components
const fetchAndIncludeComponent = async (componentName, mcp) => {
  try {
    // Fetch from MCP (pseudocode - actual implementation varies)
    const componentCode = await mcp.getComponent(componentName);
    return componentCode;
  } catch (error) {
    // Fallback to basic component
    return getFallbackComponent(componentName);
  }
};

// Caching pattern for repeated use
const componentCache = new Map();
const getCachedComponent = (name) => {
  if (!componentCache.has(name)) {
    componentCache.set(name, fetchComponent(name));
  }
  return componentCache.get(name);
};
```

### 🔄 Fallback Components
```javascript
// Always have fallbacks when MCP unavailable
const Button = shadcnButton || FallbackButton;

const FallbackButton = ({ children, variant = 'default', ...props }) => {
  const variants = {
    default: 'bg-blue-500 text-white hover:bg-blue-600',
    secondary: 'bg-gray-200 text-gray-900 hover:bg-gray-300',
    destructive: 'bg-red-500 text-white hover:bg-red-600',
    outline: 'border border-gray-300 hover:bg-gray-100'
  };
  
  return (
    <button 
      className={`px-4 py-2 rounded-md font-medium transition-colors ${variants[variant]}`}
      {...props}
    >
      {children}
    </button>
  );
};

// Fallback Card component
const FallbackCard = ({ children, className = '' }) => (
  <div className={`bg-white rounded-lg shadow-md p-6 ${className}`}>
    {children}
  </div>
);
```

### 🚨 Component Error Handling
```javascript
// Graceful degradation when MCP fails
const UIComponent = ({ component, fallback, ...props }) => {
  const [Component, setComponent] = useState(fallback);
  const [loading, setLoading] = useState(true);
  
  useEffect(() => {
    fetchComponent(component)
      .then(setComponent)
      .catch(() => console.warn(`Using fallback for ${component}`))
      .finally(() => setLoading(false));
  }, [component]);
  
  if (loading) return <SkeletonLoader />;
  return <Component {...props} />;
};
```

### ✅ Integration Best Practices
- **Always include fallbacks** - MCP might be unavailable
- **Cache components** - Don't re-fetch on every use
- **Handle loading states** - Show skeletons while fetching
- **Test offline** - Ensure app works without MCP
- **Keep components lean** - Only fetch what you need

---

*Essential patterns for Claude artifact development. Focus on what's unique to the artifact environment.*