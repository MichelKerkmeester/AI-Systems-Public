# Claude App Builder - Artifact Standards

**The single source of truth for all artifact documentation standards and patterns.**

## 📑 TABLE OF CONTENTS

1. [Header Documentation Formats](#1-header-documentation-formats)
2. [Version Requirements](#2-version-requirements)
3. [README Standards](#3-readme-standards)
4. [Session State Management](#4-session-state-management)
5. [Download & Export Patterns](#5-download--export-patterns)
6. [Clipboard Integration](#6-clipboard-integration)
7. [Simulated Features Guide](#7-simulated-features-guide)
8. [Single-File Organization](#8-single-file-organization)
9. [GitHub Sync Component](#9-github-sync-component)
10. [Quality Requirements](#10-quality-requirements)

---

## 1. HEADER DOCUMENTATION FORMATS

**Three formats available based on app complexity:**

### 📄 Minimal Format
*For simple, single-purpose apps under 100 lines*

```javascript
/**
 * App: [Name] | v[X.Y.Z] | Mode: $[mode] + [shortcuts]
 * Desc: [One sentence description]
 * Features: [Feature 1], [Feature 2], [Feature 3]
 * Usage: [One sentence on how to use]
 */
```

**Example:**
```javascript
/**
 * App: Business Name Generator | v1.0.0 | Mode: $simple
 * Desc: Generates creative business names with taglines
 * Features: Name generation, tagline creation, domain suggestions
 * Usage: Enter business description and click generate
 */
```

### 📋 Standard Format
*For most apps - balanced documentation*

```javascript
/**
 * App Name: [Clear, Descriptive Name]
 * Version: v[X.Y.Z]
 * Mode: $[mode] + [shortcuts used]
 * 
 * Description: [One sentence about what it does]
 * 
 * Features:
 * - [Feature 1]
 * - [Feature 2]
 * - [Feature 3]
 * 
 * Usage: [2-3 sentences on how to use]
 */
```

### 📚 Full Format
*For complex apps or those using external instructions*

```javascript
/**
 * App Name: [Clear, Descriptive Name]
 * Version: v[X.Y.Z]
 * Mode: $[mode] + [shortcuts used]
 * 
 * Description: [One sentence about what it does]
 * 
 * Features:
 * - [Feature 1]
 * - [Feature 2]
 * - [Feature 3]
 * 
 * UI Components:
 * - [Component Name] (Source: 21st-dev / Custom / Tailwind)
 * - [Component Name] (Source: 21st-dev / Custom / Tailwind)
 * 
 * External Instructions: [YES/NO - If YES, includes GitHub sync]
 * 
 * Usage: [2-3 sentences on how to use]
 * 
 * Technical Notes: [Any important implementation details]
 * 
 * Dependencies: [Special libraries or patterns used]
 */
```

### 🎯 Which Format to Use?

| App Complexity | Lines of Code | Format to Use |
|----------------|---------------|---------------|
| Simple tool | < 100 | Minimal |
| Standard app | 100-500 | Standard |
| Complex system | > 500 | Full |
| External instructions | Any | Full (required) |

---

## 2. VERSION REQUIREMENTS

### Semantic Versioning Rules

**Format:** `vMAJOR.MINOR.PATCH`

| Change Type | Version Part | Example | When to Use |
|-------------|--------------|---------|-------------|
| Breaking changes | MAJOR | 1.0.0 → 2.0.0 | UI completely redesigned, mode changed |
| New features | MINOR | 1.0.0 → 1.1.0 | Added search, new chart type |
| Bug fixes | PATCH | 1.0.0 → 1.0.1 | Fixed error handling, typos |

### Version History in Code

```javascript
/**
 * Version History:
 * - v1.0.0: Initial release
 * - v1.1.0: Added CSV export functionality
 * - v1.1.1: Fixed timezone handling
 * - v2.0.0: Rebuilt with $chat mode
 */
```

---

## 3. README STANDARDS

**Always create as a separate markdown artifact**

### Required Sections

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

## Source Repository
- **GitHub**: [URL if applicable]
- **Version**: [Current version]
- **Last Sync**: [Date if applicable]
```

---

## 4. SESSION STATE MANAGEMENT

### Pattern 1: Basic Session State
```javascript
// State persists during session only
const useSessionState = (key, initialValue) => {
  const [value, setValue] = useState(() => {
    // No localStorage in artifacts - just return initial
    return initialValue;
  });
  
  return [value, setValue];
};
```

### Pattern 2: Undo/Redo System
```javascript
const useUndoRedo = (initialState) => {
  const [history, setHistory] = useState([initialState]);
  const [currentIndex, setCurrentIndex] = useState(0);
  
  const setState = (newState) => {
    const newHistory = history.slice(0, currentIndex + 1);
    newHistory.push(newState);
    setHistory(newHistory);
    setCurrentIndex(newHistory.length - 1);
  };
  
  const undo = () => {
    if (currentIndex > 0) setCurrentIndex(currentIndex - 1);
  };
  
  const redo = () => {
    if (currentIndex < history.length - 1) setCurrentIndex(currentIndex + 1);
  };
  
  return {
    state: history[currentIndex],
    setState,
    undo,
    redo,
    canUndo: currentIndex > 0,
    canRedo: currentIndex < history.length - 1
  };
};
```

### Pattern 3: Complex State Management
```javascript
// For complex apps, use useReducer
const appReducer = (state, action) => {
  switch (action.type) {
    case 'SET_DATA':
      return { ...state, data: action.payload };
    case 'ADD_ITEM':
      return { ...state, items: [...state.items, action.payload] };
    case 'RESET':
      return initialState;
    default:
      return state;
  }
};

// Usage
const [state, dispatch] = useReducer(appReducer, initialState);
```

---

## 5. DOWNLOAD & EXPORT PATTERNS

### Pattern 1: Text/JSON Download
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

### Pattern 2: Canvas/Chart Export
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

### Pattern 3: CSV Generation
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

## 6. CLIPBOARD INTEGRATION

### Pattern 1: Copy to Clipboard
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

### Pattern 2: Rich Content Copy
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

## 7. SIMULATED FEATURES GUIDE

### Pattern 1: Simulated Authentication
```javascript
const SimulatedAuth = () => {
  const [user, setUser] = useState(null);
  const [loading, setLoading] = useState(false);
  
  const login = async (username, password) => {
    setLoading(true);
    // Simulate API call
    await new Promise(r => setTimeout(r, 1000));
    
    // Always succeed for demo
    setUser({
      id: Date.now(),
      username,
      role: 'user',
      token: btoa(`${username}:${Date.now()}`)
    });
    setLoading(false);
  };
  
  const logout = () => {
    setUser(null);
  };
  
  return { user, login, logout, loading };
};
```

### Pattern 2: Simulated Database
```javascript
const useSimulatedDB = () => {
  const [data, setData] = useState([]);
  const [loading, setLoading] = useState(false);
  
  const query = async (filter = {}) => {
    setLoading(true);
    await new Promise(r => setTimeout(r, 300));
    
    const filtered = data.filter(item => {
      return Object.entries(filter).every(([key, value]) => 
        item[key] === value
      );
    });
    
    setLoading(false);
    return filtered;
  };
  
  const insert = async (item) => {
    setLoading(true);
    await new Promise(r => setTimeout(r, 200));
    
    const newItem = {
      ...item,
      id: Date.now(),
      createdAt: new Date().toISOString()
    };
    
    setData(prev => [...prev, newItem]);
    setLoading(false);
    return newItem;
  };
  
  return { query, insert, loading };
};
```

### Pattern 3: Simulated Real-time Updates
```javascript
const useSimulatedRealtime = (eventType, callback) => {
  useEffect(() => {
    // Simulate random events
    const interval = setInterval(() => {
      if (Math.random() > 0.7) {
        callback({
          type: eventType,
          data: generateMockEvent(),
          timestamp: Date.now()
        });
      }
    }, 3000);
    
    return () => clearInterval(interval);
  }, [eventType, callback]);
};
```

---

## 8. SINGLE-FILE ORGANIZATION

### Pattern 1: Component Organization
```javascript
// For large single-file apps, organize with clear sections

// ============================================
// IMPORTS & CONSTANTS
// ============================================
import React, { useState, useEffect } from 'react';
import { ... } from 'lucide-react';

const CONSTANTS = {
  API_TIMEOUT: 5000,
  MAX_RETRIES: 3
};

// ============================================
// UTILITY FUNCTIONS
// ============================================
const utils = {
  formatDate: (date) => { /* ... */ },
  parseData: (raw) => { /* ... */ }
};

// ============================================
// CUSTOM HOOKS
// ============================================
const useAppState = () => { /* ... */ };
const useClaudeAPI = () => { /* ... */ };

// ============================================
// SUB-COMPONENTS
// ============================================
const Header = ({ title, user }) => { /* ... */ };
const Sidebar = ({ items, onSelect }) => { /* ... */ };
const MainContent = ({ data }) => { /* ... */ };

// ============================================
// MAIN COMPONENT
// ============================================
export default function App() {
  // Main app logic here
}
```

### Pattern 2: Feature Modules
```javascript
// Group related functionality
const FeatureModules = {
  // Authentication module
  auth: {
    login: async (credentials) => { /* ... */ },
    logout: () => { /* ... */ },
    checkAuth: () => { /* ... */ }
  },
  
  // Data processing module  
  dataProcessor: {
    parse: (raw) => { /* ... */ },
    validate: (data) => { /* ... */ },
    transform: (data) => { /* ... */ }
  },
  
  // UI helpers module
  ui: {
    showToast: (message) => { /* ... */ },
    confirm: (message) => { /* ... */ },
    formatters: { /* ... */ }
  }
};
```

### Pattern 3: State Structure
```javascript
// For complex state, use a clear structure
const initialState = {
  // UI State
  ui: {
    loading: false,
    error: null,
    activeView: 'dashboard',
    sidebarOpen: true
  },
  
  // Domain Data
  data: {
    items: [],
    selectedId: null,
    filters: {}
  },
  
  // User/Session
  session: {
    user: null,
    preferences: {}
  },
  
  // Temporary/Form State
  temp: {
    formData: {},
    validationErrors: {}
  }
};
```

---

## 9. GITHUB SYNC COMPONENT

### Complete Implementation
```javascript
import { GitBranch, CheckCircle, AlertCircle, Upload } from 'lucide-react';

const GitHubSyncStatus = ({ 
  systemName, 
  currentVersion, 
  githubUrl, 
  isPublicRepo = true,
  onInstructionsUpdate 
}) => {
  const [status, setStatus] = useState('idle');
  const [showUploadModal, setShowUploadModal] = useState(false);
  
  const checkForUpdates = async () => {
    if (!isPublicRepo) {
      setShowUploadModal(true);
      return;
    }
    
    setStatus('checking');
    try {
      // In real implementation: Use search MCP to check GitHub
      // Simulated for now
      await new Promise(r => setTimeout(r, 2000));
      setStatus('synced');
    } catch (err) {
      setStatus('error');
    }
  };
  
  const handleFileUpload = async (file) => {
    try {
      const content = await file.text();
      if (onInstructionsUpdate) {
        onInstructionsUpdate(content);
      }
      setShowUploadModal(false);
      setStatus('synced');
    } catch (err) {
      setStatus('error');
    }
  };
  
  return (
    <>
      <div className="fixed bottom-4 right-4 bg-white rounded-lg shadow-lg p-3 flex items-center gap-3">
        {status === 'idle' && <GitBranch className="w-4 h-4 text-gray-400" />}
        {status === 'checking' && <div className="w-4 h-4 animate-spin">⟳</div>}
        {status === 'synced' && <CheckCircle className="w-4 h-4 text-green-500" />}
        {status === 'error' && <AlertCircle className="w-4 h-4 text-red-500" />}
        
        <div className="text-sm">
          <div className="font-medium">{systemName}</div>
          <div className="text-gray-500">v{currentVersion}</div>
        </div>
        
        <button
          onClick={checkForUpdates}
          className="p-2 hover:bg-gray-100 rounded-md"
          title={isPublicRepo ? "Check for updates" : "Upload instructions"}
        >
          {isPublicRepo ? '↻' : <Upload className="w-4 h-4" />}
        </button>
      </div>
      
      {/* Upload Modal for Private Repos */}
      {showUploadModal && (
        <div className="fixed inset-0 bg-black/50 flex items-center justify-center z-50">
          <div className="bg-white rounded-lg p-6 max-w-md w-full">
            <h3 className="text-lg font-semibold mb-4">Upload Instructions</h3>
            <input
              type="file"
              accept=".md,.txt,.json"
              onChange={(e) => handleFileUpload(e.target.files[0])}
              className="mb-4"
            />
            <button
              onClick={() => setShowUploadModal(false)}
              className="px-4 py-2 bg-gray-200 rounded"
            >
              Cancel
            </button>
          </div>
        </div>
      )}
    </>
  );
};
```

---

## 10. QUALITY REQUIREMENTS

### Must-Have Checklist

- [ ] **Works immediately** - No setup or configuration needed
- [ ] **Header documentation** - Uses one of the three formats
- [ ] **Error handling** - All async operations have try/catch
- [ ] **Loading states** - Every async operation shows feedback
- [ ] **Mobile responsive** - Works on all screen sizes
- [ ] **Keyboard accessible** - Tab navigation works
- [ ] **Clear UI** - Intuitive without instructions
- [ ] **Fast performance** - No unnecessary re-renders
- [ ] **Graceful degradation** - Works when MCPs unavailable

### Performance Patterns

```javascript
// Memo expensive components
const ExpensiveComponent = React.memo(({ data }) => {
  return <div>{/* Complex rendering */}</div>
});

// Optimize expensive calculations
const processedData = useMemo(() => {
  return expensiveCalculation(rawData);
}, [rawData]);

// Stable callbacks
const handleClick = useCallback(() => {
  doSomething(id);
}, [id]);

// Debounced inputs
const DebouncedInput = ({ onSearch }) => {
  const [value, setValue] = useState('');
  
  useEffect(() => {
    const timer = setTimeout(() => {
      onSearch(value);
    }, 300);
    
    return () => clearTimeout(timer);
  }, [value, onSearch]);
  
  return <input value={value} onChange={e => setValue(e.target.value)} />;
};
```

### Error Boundary Pattern

```javascript
class ErrorBoundary extends React.Component {
  state = { hasError: false };
  
  static getDerivedStateFromError(error) {
    return { hasError: true };
  }
  
  componentDidCatch(error, errorInfo) {
    console.error('Error caught:', error, errorInfo);
  }
  
  render() {
    if (this.state.hasError) {
      return (
        <div className="p-8 text-center">
          <h2 className="text-xl font-semibold mb-2">Something went wrong</h2>
          <button 
            onClick={() => window.location.reload()}
            className="px-4 py-2 bg-blue-500 text-white rounded"
          >
            Reload App
          </button>
        </div>
      );
    }
    
    return this.props.children;
  }
}

// Usage: Wrap your app
<ErrorBoundary>
  <App />
</ErrorBoundary>
```

---

*This document is the single source of truth for Claude App Builder standards. All apps must follow these patterns for consistency and quality.*