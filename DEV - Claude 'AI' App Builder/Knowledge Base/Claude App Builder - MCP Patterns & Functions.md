# Claude App Builder - MCP Patterns & Functions

**The comprehensive guide to integrating Model Context Protocol features in Claude AI apps.**

## 📑 TABLE OF CONTENTS

1. [🔌 Understanding MCP Integration](#1-understanding-mcp-integration)
2. [📚 Available MCPs Reference](#2-available-mcps-reference)
3. [⌨️ User Shortcuts to MCP Mapping](#3-user-shortcuts-to-mcp-mapping)
4. [🔧 MCP Integration Patterns](#4-mcp-integration-patterns)
5. [📦 Handling MCP Results](#5-handling-mcp-results)
   - [5.1 Search Results Integration](#51-search-results-integration)
   - [5.2 Documentation Display](#52-documentation-display)
   - [5.3 UI Component Integration](#53-ui-component-integration)
   - [5.4 Download & Export Patterns](#54-download--export-patterns)
   - [5.5 Clipboard Integration](#55-clipboard-integration)
   - [5.6 Session State Management](#56-session-state-management)
6. [⚡ Mode + MCP Combinations](#6-mode--mcp-combinations)
7. [🎨 UI Component Strategy](#7-ui-component-strategy)
8. [🛡️ MCP Limitations & Fallbacks](#8-mcp-limitations--fallbacks)
9. [🚀 Performance & State Management](#9-performance--state-management)
10. [🧪 Testing MCP Integration](#10-testing-mcp-integration)
11. [🗂️ Single-File Organization with MCPs](#11-single-file-organization-with-mcps)
12. [📋 Quick Reference](#12-quick-reference)
    - [12.1 Essential Imports](#121-essential-imports-for-mcp-apps)
    - [12.2 MCP Cheat Sheet](#122-mcp-cheat-sheet)
    - [12.3 Common Patterns](#123-common-patterns-quick-copy)
    - [12.4 Final Quality Checklist](#124-final-quality-checklist)

---

## 🔌 1. UNDERSTANDING MCP INTEGRATION

**Context:** This document guides how Claude should integrate MCP (Model Context Protocol) functionality when building apps. Users request features via shortcuts, and Claude implements them using available MCPs.

### Key Principles:
- Users specify desired features with `$shortcuts`
- Claude determines which MCPs to use
- **Code reasoning is MANDATORY for every app build**
- All MCP results must be integrated seamlessly into the app
- Gracefully handle unavailable MCPs with fallbacks
- Session-only state management (no localStorage)

### Version History
- v2.0.0 (Current): Added mandatory code-reasoning, enhanced error handling, new state patterns
- v1.0.0: Initial MCP integration patterns

### Environment Constraints
| Feature | Status | MCP Alternative |
|---------|--------|-----------------|
| localStorage | ❌ | Session state in React |
| External APIs | ❌ | MCP calls only |
| Server-side | ❌ | Client-side MCPs only |
| File system | ❌ | window.fs.readFile only |
| Background workers | ❌ | Main thread MCPs |

---

## 📚 2. AVAILABLE MCPS REFERENCE

### Core MCPs for App Building:

| MCP | Purpose | When to Use | Priority |
|-----|---------|-------------|----------|
| **`code-reasoning:code-reasoning`** 🧠 | Optimize approach | **EVERY APP BUILD** | **MANDATORY** |
| `sequential-thinking:sequentialthinking` | Complex planning | Multi-step problems | High |
| `@21st-dev/magic:21st_magic_component_builder` | UI components | User requests premium UI | High |
| `@21st-dev/magic:logo_search` | Brand logos | Need company logos | Medium |
| `@21st-dev/magic:21st_magic_component_refiner` | Improve UI | Refining existing components | Medium |
| `tavily:search` | Web search | Current information needed | High |
| `brave-search:brave_web_search` | Alternative search | Backup for Tavily | High |
| `context7:resolve-library-id` | Find library | First step for docs | High |
| `context7:get-library-docs` | Get documentation | Fetch library docs | High |

### 🧠 MANDATORY: Code Reasoning
```javascript
// MUST use for EVERY app build - no exceptions
await codeReasoning({
  thought: "Analyzing best approach for [app type]",
  thoughtNumber: 1,
  totalThoughts: 5, // Adjust based on complexity
  nextThoughtNeeded: true
});
```

### Available Libraries in Artifacts
```javascript
// Core React
import React, { useState, useEffect, useRef, useMemo, useCallback, useReducer } from 'react';

// Icons (Lucide React)
import { Search, Loader2, AlertCircle, CheckCircle, X, Plus } from 'lucide-react';

// Data Visualization
import { LineChart, BarChart, PieChart, Line, Bar, Pie, XAxis, YAxis, CartesianGrid, Tooltip, Legend } from 'recharts';

// Utilities
import _ from 'lodash';
import Papa from 'papaparse';
import * as XLSX from 'xlsx';
import * as math from 'mathjs';
import * as d3 from 'd3';

// Also available: Plotly, Chart.js, Three.js (r128), Tone.js, TensorFlow.js
```

---

## ⌨️ 3. USER SHORTCUTS TO MCP MAPPING

### Shortcut Reference Table

| User Shortcut | Feature to Implement | MCPs to Use | Implementation Notes |
|---------------|---------------------|-------------|---------------------|
| `$search` | Current web data access | `tavily:search`, `brave-search:brave_web_search` | Integrate search results into app UI |
| `$docs` | Library documentation | `context7:resolve-library-id`, `context7:get-library-docs` | Fetch and display relevant docs |
| `$21` or `/ui` | Premium UI components | `@21st-dev/magic:21st_magic_component_builder` | Request UI components from catalog |
| `$logo` | Company logos | `@21st-dev/magic:logo_search` | Fetch brand logos in JSX/TSX/SVG |

### Implementation Examples:

**When user says:** `"Build a $chat bot with $search"`
**Claude should:**
1. Use code-reasoning to optimize approach (MANDATORY)
2. Create chat interface ($chat mode)
3. Add search capability using Tavily/Brave MCPs
4. Integrate search results into chat responses

**When user says:** `"$simple tool with $docs for React hooks"`
**Claude should:**
1. Use code-reasoning to plan implementation (MANDATORY)
2. Create simple tool interface
3. Use Context7 to fetch React documentation
4. Display relevant hook information in UI

---

## 🔧 4. MCP INTEGRATION PATTERNS

### Core Error Handler Implementation
```javascript
// Complete MCPErrorHandler with exponential backoff
const MCPErrorHandler = {
  config: {
    maxRetries: 3,
    baseDelay: 1000,
    maxDelay: 10000,
    timeout: 30000
  },
  
  async withFallback(mcpCall, fallbackFn, options = {}) {
    const { 
      retries = this.config.maxRetries,
      showNotification = true 
    } = options;
    
    let lastError;
    
    for (let attempt = 0; attempt <= retries; attempt++) {
      try {
        // Create timeout promise
        const timeoutPromise = new Promise((_, reject) => 
          setTimeout(() => reject(new Error('MCP timeout')), this.config.timeout)
        );
        
        // Race between MCP call and timeout
        const result = await Promise.race([mcpCall(), timeoutPromise]);
        return result;
        
      } catch (error) {
        lastError = error;
        
        if (attempt === retries) {
          // All retries exhausted
          if (showNotification) {
            this.showNotification('Feature temporarily unavailable');
          }
          
          // Execute fallback
          if (fallbackFn) {
            return await fallbackFn();
          }
          
          throw error;
        }
        
        // Calculate delay with exponential backoff
        const delay = Math.min(
          this.config.baseDelay * Math.pow(2, attempt),
          this.config.maxDelay
        );
        
        await new Promise(r => setTimeout(r, delay));
      }
    }
  },
  
  showNotification(message) {
    const notification = document.createElement('div');
    notification.className = 'fixed top-4 right-4 bg-yellow-100 text-yellow-800 px-4 py-3 rounded-lg shadow-lg z-50';
    notification.textContent = message;
    document.body.appendChild(notification);
    
    setTimeout(() => notification.remove(), 5000);
  }
};
```

### Pattern 1: Search Integration with Complete Error Handling
```javascript
const SearchFeature = () => {
  const [searchResults, setSearchResults] = useState(null);
  const [loading, setLoading] = useState(false);
  const [error, setError] = useState(null);
  
  const performSearch = async (query) => {
    setLoading(true);
    setError(null);
    
    try {
      const results = await MCPErrorHandler.withFallback(
        async () => {
          const response = await tavily.search({
            query,
            options: { maxResults: 10, includeAnswer: true }
          });
          return response;
        },
        async () => {
          // Fallback to Brave search
          const response = await braveSearch.webSearch({
            query,
            count: 10
          });
          return response;
        },
        { retries: 2, showNotification: true }
      );
      
      setSearchResults(processSearchResults(results));
    } catch (err) {
      setError('Search temporarily unavailable');
      // Use simulated results
      const simulated = await SimulatedMCPResponses.search(query);
      setSearchResults(simulated);
    } finally {
      setLoading(false);
    }
  };
  
  return (
    <div>
      {loading && <SkeletonLoader />}
      {error && <ErrorDisplay message={error} />}
      {searchResults && <ResultsDisplay results={searchResults} />}
    </div>
  );
};
```

### Pattern 2: Documentation Integration with Session State
```javascript
const DocsFeature = () => {
  // Session state using React (no localStorage)
  const [docsCache, setDocsCache] = useState(new Map());
  const [currentDocs, setCurrentDocs] = useState(null);
  
  const fetchDocs = async (library) => {
    // Check session cache first
    if (docsCache.has(library)) {
      setCurrentDocs(docsCache.get(library));
      return;
    }
    
    try {
      const docs = await MCPErrorHandler.withFallback(
        async () => {
          // 1. Resolve library ID
          const resolved = await context7.resolveLibraryId({
            libraryName: library
          });
          
          // 2. Fetch documentation
          const docs = await context7.getLibraryDocs({
            context7CompatibleLibraryID: resolved[0].id,
            tokens: 10000
          });
          
          return docs;
        },
        async () => {
          // Fallback to simulated docs
          return SimulatedMCPResponses.docs(library);
        }
      );
      
      // Cache in session state
      const newCache = new Map(docsCache);
      newCache.set(library, docs);
      setDocsCache(newCache);
      setCurrentDocs(docs);
      
    } catch (err) {
      setCurrentDocs({
        fallback: true,
        message: 'Documentation unavailable',
        externalLink: `https://docs.${library}.com`
      });
    }
  };
  
  return <DocsViewer docs={currentDocs} />;
};
```

### Pattern 3: UI Component Integration with Animations
```javascript
const PremiumUIApp = () => {
  const [components, setComponents] = useState([]);
  const [loading, setLoading] = useState(false);
  
  const fetchPremiumComponents = async (componentType) => {
    setLoading(true);
    
    try {
      const result = await MCPErrorHandler.withFallback(
        async () => {
          return await magic21st.componentBuilder({
            searchQuery: componentType,
            message: `Build a ${componentType} component`,
            standaloneRequestQuery: `Modern, animated ${componentType}`,
            absolutePathToCurrentFile: '/app.jsx',
            absolutePathToProjectDirectory: '/'
          });
        },
        async () => {
          // Fallback to custom component
          return buildCustomComponent(componentType);
        }
      );
      
      // Integrate with smooth transitions
      setComponents(prev => [...prev, {
        ...result,
        id: Date.now(),
        animation: 'slide-in-from-bottom'
      }]);
      
    } finally {
      setLoading(false);
    }
  };
  
  return (
    <div className="space-y-4">
      {components.map((comp, index) => (
        <SmoothTransition
          key={comp.id}
          show={true}
          delay={index * 100}
        >
          <ComponentRenderer component={comp} />
        </SmoothTransition>
      ))}
    </div>
  );
};
```

### UI Component Implementations
```javascript
// Skeleton Loader Component (from Examples & Patterns)
const SkeletonLoader = ({ variant = 'text', className = '' }) => {
  const baseClass = 'animate-pulse bg-gray-200 rounded';
  
  const variants = {
    text: 'h-4 w-full',
    title: 'h-8 w-3/4',
    avatar: 'h-12 w-12 rounded-full',
    image: 'h-48 w-full',
    button: 'h-10 w-24'
  };
  
  return <div className={`${baseClass} ${variants[variant]} ${className}`} />;
};

// Smooth Transition Component (from Examples & Patterns)
const SmoothTransition = ({ 
  children, 
  show, 
  delay = 0,
  duration = 300,
  enterFrom = 'opacity-0 scale-95',
  enterTo = 'opacity-100 scale-100'
}) => {
  const [shouldRender, setShouldRender] = useState(show);
  const [animationClass, setAnimationClass] = useState('');
  
  useEffect(() => {
    if (show) {
      setShouldRender(true);
      setTimeout(() => {
        setAnimationClass(`${enterTo} transition-all duration-${duration}`);
      }, delay);
    } else {
      setAnimationClass(`${enterFrom} transition-all duration-${duration}`);
      setTimeout(() => setShouldRender(false), duration + delay);
    }
  }, [show, delay, duration, enterFrom, enterTo]);
  
  if (!shouldRender) return null;
  
  return <div className={animationClass}>{children}</div>;
};
```

---

## 📦 5. HANDLING MCP RESULTS

### 5.1 Search Results Integration
```javascript
// Transform search results into app-friendly format
const processSearchResults = (mcpResults) => {
  return {
    summary: extractSummary(mcpResults),
    sources: formatSources(mcpResults),
    relevantData: parseRelevantInfo(mcpResults),
    timestamp: new Date().toISOString()
  };
};

const extractSummary = (results) => {
  if (results.answer) return results.answer;
  if (results.results?.[0]?.content) return results.results[0].content.slice(0, 200) + '...';
  return 'No summary available';
};

const formatSources = (results) => {
  const sources = results.results || [];
  return sources.map(source => ({
    title: source.title,
    url: source.url,
    snippet: source.content || source.description
  }));
};
```

### 5.2 Documentation Display
```javascript
// Format docs for in-app display
const processDocumentation = (mcpDocs) => {
  return {
    overview: mcpDocs.summary || mcpDocs.content?.slice(0, 500),
    examples: extractCodeExamples(mcpDocs),
    reference: mcpDocs.apiReference || null,
    searchable: createSearchableIndex(mcpDocs)
  };
};

const extractCodeExamples = (docs) => {
  const codeBlocks = docs.content?.match(/```[\s\S]*?```/g) || [];
  return codeBlocks.map(block => ({
    code: block.replace(/```\w*\n?|```$/g, ''),
    language: block.match(/```(\w+)/)?.[1] || 'javascript'
  }));
};
```

### 5.3 UI Component Integration
```javascript
// Integrate fetched components
const integrateUIComponent = (mcpComponent) => {
  // Adapt component to app's needs
  return {
    ...mcpComponent,
    props: adaptPropsToApp(mcpComponent.props),
    styles: mergeWithAppTheme(mcpComponent.styles),
    animations: enhanceWithTransitions(mcpComponent)
  };
};

const adaptPropsToApp = (props) => {
  // Ensure props match app's data structure
  return {
    ...props,
    className: `${props.className || ''} app-component`,
    'data-mcp-source': '21st-dev'
  };
};
```

### 5.4 Download & Export Patterns
```javascript
// Download MCP results as files
const DownloadMCPResults = ({ results, format }) => {
  const downloadResults = () => {
    let content, mimeType, filename;
    
    switch (format) {
      case 'json':
        content = JSON.stringify(results, null, 2);
        mimeType = 'application/json';
        filename = 'mcp-results.json';
        break;
      case 'csv':
        content = convertToCSV(results);
        mimeType = 'text/csv';
        filename = 'mcp-results.csv';
        break;
      case 'markdown':
        content = convertToMarkdown(results);
        mimeType = 'text/markdown';
        filename = 'mcp-results.md';
        break;
    }
    
    const blob = new Blob([content], { type: mimeType });
    const url = URL.createObjectURL(blob);
    const link = document.createElement('a');
    link.href = url;
    link.download = filename;
    link.click();
    URL.revokeObjectURL(url);
  };
  
  return (
    <button onClick={downloadResults} className="download-btn">
      <Download className="w-4 h-4" />
      Export {format.toUpperCase()}
    </button>
  );
};

// Helper functions
const convertToCSV = (results) => {
  if (Array.isArray(results)) {
    return Papa.unparse(results);
  }
  // Convert object to CSV
  return Papa.unparse([results]);
};

const convertToMarkdown = (results) => {
  let md = '# MCP Results\n\n';
  
  if (results.summary) {
    md += `## Summary\n\n${results.summary}\n\n`;
  }
  
  if (results.sources) {
    md += '## Sources\n\n';
    results.sources.forEach(source => {
      md += `- [${source.title}](${source.url})\n`;
      md += `  ${source.snippet}\n\n`;
    });
  }
  
  return md;
};
```

### 5.5 Clipboard Integration
```javascript
// Copy MCP results to clipboard
const CopyMCPResults = ({ results, format = 'text' }) => {
  const [copied, setCopied] = useState(false);
  
  const copyToClipboard = async () => {
    let content;
    
    try {
      switch (format) {
        case 'json':
          content = JSON.stringify(results, null, 2);
          break;
        case 'markdown':
          content = convertToMarkdown(results);
          break;
        default:
          content = convertToPlainText(results);
      }
      
      await navigator.clipboard.writeText(content);
      setCopied(true);
      setTimeout(() => setCopied(false), 2000);
      
    } catch (err) {
      // Fallback method for older browsers
      const textarea = document.createElement('textarea');
      textarea.value = content;
      textarea.style.position = 'fixed';
      textarea.style.opacity = '0';
      document.body.appendChild(textarea);
      textarea.select();
      
      try {
        document.execCommand('copy');
        setCopied(true);
        setTimeout(() => setCopied(false), 2000);
      } catch (e) {
        console.error('Clipboard copy failed:', e);
      } finally {
        document.body.removeChild(textarea);
      }
    }
  };
  
  return (
    <button 
      onClick={copyToClipboard}
      className={`inline-flex items-center gap-2 px-3 py-2 rounded-lg transition-colors ${
        copied ? 'bg-green-100 text-green-700' : 'bg-gray-100 hover:bg-gray-200'
      }`}
    >
      {copied ? (
        <>
          <CheckCircle className="w-4 h-4" />
          Copied!
        </>
      ) : (
        <>
          <Copy className="w-4 h-4" />
          Copy
        </>
      )}
    </button>
  );
};

const convertToPlainText = (results) => {
  if (typeof results === 'string') return results;
  
  let text = '';
  if (results.summary) text += results.summary + '\n\n';
  if (results.sources) {
    text += 'Sources:\n';
    results.sources.forEach(s => {
      text += `- ${s.title}: ${s.url}\n`;
    });
  }
  return text;
};
```

### 5.6 Session State Management
```javascript
// Session-only state for MCP results (no localStorage)
const useMCPSessionState = (key, initialValue) => {
  // Store in React state only - cleared on page refresh
  const [sessionData, setSessionData] = useState(() => {
    return {
      [key]: initialValue,
      timestamp: Date.now(),
      sessionId: Math.random().toString(36).substr(2, 9)
    };
  });
  
  const updateSessionData = (newValue) => {
    setSessionData(prev => ({
      ...prev,
      [key]: newValue,
      lastUpdated: Date.now()
    }));
  };
  
  // Provide session info
  const getSessionInfo = () => ({
    created: new Date(sessionData.timestamp),
    lastUpdated: new Date(sessionData.lastUpdated || sessionData.timestamp),
    sessionId: sessionData.sessionId
  });
  
  return [sessionData[key], updateSessionData, getSessionInfo];
};

// Undo/Redo pattern for MCP results
const useMCPUndoRedo = (initialState) => {
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

---

## ⚡ 6. MODE + MCP COMBINATIONS

### Common Combinations with Complete Examples

#### `$chat + $search` - Full Implementation
```javascript
// Conversational interface with web search
const ChatWithSearch = () => {
  const [messages, setMessages] = useState([]);
  const [input, setInput] = useState('');
  const [searching, setSearching] = useState(false);
  
  const handleMessage = async (userMessage) => {
    // Add user message
    setMessages(prev => [...prev, { 
      id: Date.now(),
      role: 'user', 
      content: userMessage 
    }]);
    
    // Check if search needed
    if (needsCurrentInfo(userMessage)) {
      setSearching(true);
      
      try {
        const searchResults = await MCPErrorHandler.withFallback(
          async () => {
            return await tavily.search({
              query: extractSearchQuery(userMessage),
              options: { maxResults: 5, includeAnswer: true }
            });
          },
          async () => SimulatedMCPResponses.search(userMessage)
        );
        
        // Generate response with search context
        const response = await generateResponseWithSearch(userMessage, searchResults);
        
        setMessages(prev => [...prev, { 
          id: Date.now() + 1,
          role: 'assistant', 
          content: response,
          sources: searchResults.results
        }]);
      } finally {
        setSearching(false);
      }
    }
  };
  
  const needsCurrentInfo = (message) => {
    const triggers = ['latest', 'current', 'today', 'news', 'price', 'weather'];
    return triggers.some(trigger => message.toLowerCase().includes(trigger));
  };
  
  const extractSearchQuery = (message) => {
    // Extract the main query from the message
    return message.replace(/^(what|who|when|where|why|how|is|are|can you tell me about)/i, '').trim();
  };
  
  return (
    <div className="flex flex-col h-screen">
      <div className="flex-1 overflow-y-auto p-4 space-y-4">
        {messages.map(msg => (
          <MessageBubble key={msg.id} message={msg} />
        ))}
        {searching && <SearchingIndicator />}
      </div>
      
      <div className="border-t p-4">
        <div className="flex gap-2">
          <input
            type="text"
            value={input}
            onChange={(e) => setInput(e.target.value)}
            onKeyPress={(e) => e.key === 'Enter' && handleMessage(input)}
            placeholder="Ask me anything..."
            className="flex-1 px-4 py-2 border rounded-lg"
            disabled={searching}
          />
          <button
            onClick={() => handleMessage(input)}
            disabled={!input.trim() || searching}
            className="px-4 py-2 bg-blue-500 text-white rounded-lg disabled:opacity-50"
          >
            Send
          </button>
        </div>
      </div>
    </div>
  );
};
```

#### `$analyze + $docs` - Full Implementation
```javascript
// Data analysis with documentation support
const AnalyzeWithDocs = () => {
  const [data, setData] = useState(null);
  const [analysis, setAnalysis] = useState(null);
  const [relevantDocs, setRelevantDocs] = useState(null);
  const [activeLibrary, setActiveLibrary] = useState(null);
  
  // Auto-detect libraries from data
  useEffect(() => {
    if (data) {
      const libraries = detectLibraries(data);
      if (libraries.length > 0) {
        fetchDocsForLibrary(libraries[0]);
      }
    }
  }, [data]);
  
  const detectLibraries = (data) => {
    const libraries = [];
    
    // Check for pandas-like operations
    if (data.columns && data.dtypes) libraries.push('pandas');
    
    // Check for numpy arrays
    if (data.shape && data.dtype) libraries.push('numpy');
    
    // Check for React components
    if (data.components) libraries.push('react');
    
    return libraries;
  };
  
  const fetchDocsForLibrary = async (library) => {
    setActiveLibrary(library);
    
    try {
      const docs = await MCPErrorHandler.withFallback(
        async () => {
          const resolved = await context7.resolveLibraryId({ 
            libraryName: library 
          });
          
          return await context7.getLibraryDocs({
            context7CompatibleLibraryID: resolved[0].id,
            tokens: 10000,
            topic: 'data analysis'
          });
        },
        async () => SimulatedMCPResponses.docs(library)
      );
      
      setRelevantDocs(processDocumentation(docs));
    } catch (err) {
      console.error('Docs fetch failed:', err);
    }
  };
  
  const runAnalysis = async () => {
    if (!data) return;
    
    // Use Claude API for analysis
    const prompt = `
      Analyze this data and provide insights:
      ${JSON.stringify(data, null, 2).slice(0, 1000)}
      
      ${relevantDocs ? `Using ${activeLibrary} best practices from docs.` : ''}
      
      Provide:
      {
        "summary": "key findings",
        "patterns": ["pattern1", "pattern2"],
        "recommendations": ["rec1", "rec2"],
        "visualizations": ["suggested charts"]
      }
    `;
    
    const result = await claudeAPI.call(prompt);
    setAnalysis(result.data);
  };
  
  return (
    <div className="grid grid-cols-3 gap-4 h-screen">
      <div className="col-span-2 p-6">
        <DataUploader onDataLoad={setData} />
        {data && (
          <>
            <DataPreview data={data} />
            <button onClick={runAnalysis} className="mt-4 px-4 py-2 bg-blue-500 text-white rounded">
              Analyze Data
            </button>
            {analysis && <AnalysisResults analysis={analysis} />}
          </>
        )}
      </div>
      
      <div className="border-l p-6 overflow-y-auto">
        <h3 className="font-semibold mb-4">Documentation Helper</h3>
        {relevantDocs ? (
          <DocsPanel docs={relevantDocs} library={activeLibrary} />
        ) : (
          <p className="text-gray-500">Documentation will appear when relevant libraries are detected</p>
        )}
      </div>
    </div>
  );
};
```

### Implementation Priority:
1. **Always start with code-reasoning** (MANDATORY)
2. Build core mode functionality
3. Layer in MCP features based on shortcuts
4. Ensure seamless integration
5. Test with and without MCP availability

---

## 🎨 7. UI COMPONENT STRATEGY

### When User Requests UI Components:

1. **With `$21` or `/ui` shortcut:**
```javascript
const PremiumUIStrategy = async (componentNeeds) => {
  const components = [];
  
  for (const need of componentNeeds) {
    try {
      // Attempt to fetch from 21st-dev catalog
      const component = await MCPErrorHandler.withFallback(
        async () => {
          return await magic21st.componentBuilder({
            searchQuery: need.type,
            message: need.description,
            standaloneRequestQuery: need.requirements,
            absolutePathToCurrentFile: '/app.jsx',
            absolutePathToProjectDirectory: '/'
          });
        },
        async () => {
          // Fallback to custom component
          return buildCustomComponent(need);
        },
        { retries: 1 }
      );
      
      components.push(component);
    } catch (err) {
      console.error(`Failed to fetch ${need.type}:`, err);
      components.push(buildCustomComponent(need));
    }
  }
  
  return components;
};

// Custom component builder
const buildCustomComponent = (need) => {
  const components = {
    'pricing-card': buildPricingCard,
    'hero-section': buildHeroSection,
    'feature-grid': buildFeatureGrid,
    'testimonial': buildTestimonial
  };
  
  const builder = components[need.type] || buildGenericComponent;
  return builder(need);
};

const buildPricingCard = (need) => ({
  component: `
    const PricingCard = ({ plan, price, features, highlighted }) => (
      <div className={\`p-6 rounded-xl border-2 transition-all \${
        highlighted ? 'border-blue-500 shadow-xl' : 'border-gray-200'
      }\`}>
        <h3 className="text-xl font-bold">{plan}</h3>
        <p className="text-3xl font-bold mt-2">${price}<span className="text-base">/mo</span></p>
        <ul className="mt-4 space-y-2">
          {features.map((f, i) => (
            <li key={i} className="flex items-center gap-2">
              <CheckCircle className="w-4 h-4 text-green-500" />
              {f}
            </li>
          ))}
        </ul>
        <button className={\`w-full mt-6 py-2 rounded-lg font-medium \${
          highlighted ? 'bg-blue-500 text-white' : 'bg-gray-100'
        }\`}>
          Get Started
        </button>
      </div>
    );
  `,
  imports: ['import { CheckCircle } from "lucide-react";'],
  usage: 'For pricing tables and subscription tiers'
});
```

2. **Without UI shortcuts:**
```javascript
const StandardUIStrategy = (componentNeeds) => {
  // Build custom React components with Tailwind
  return componentNeeds.map(need => ({
    component: createReactComponent(need),
    styles: generateTailwindClasses(need),
    animations: need.animated ? addCSSTransitions(need) : null
  }));
};

const createReactComponent = (need) => {
  // Generate component based on need
  switch (need.type) {
    case 'form':
      return createFormComponent(need);
    case 'table':
      return createTableComponent(need);
    case 'chart':
      return createChartComponent(need);
    default:
      return createGenericComponent(need);
  }
};
```

3. **Component Selection Flow:**
```
User mentions UI need?
├─ Includes $21 or /ui? → Fetch from 21st-dev catalog
├─ Complex component needed? → Build custom with React
└─ Simple component? → Use basic HTML + Tailwind

Always ensure:
- Mobile responsive
- Accessible (ARIA labels)
- Smooth animations
- Error states
- Loading states
```

---

## 🛡️ 8. MCP LIMITATIONS & FALLBACKS

### Common Limitations:
1. **Availability** - MCP might be temporarily unavailable
2. **Rate limits** - Some MCPs have usage limits  
3. **Response time** - Network delays possible
4. **Data freshness** - Search results may have delays

### Error Boundaries for MCPs
```javascript
// MCP-specific error boundary
class MCPErrorBoundary extends React.Component {
  constructor(props) {
    super(props);
    this.state = { hasError: false, error: null };
  }
  
  static getDerivedStateFromError(error) {
    return { hasError: true, error };
  }
  
  componentDidCatch(error, errorInfo) {
    console.error('MCP Error:', error, errorInfo);
    
    // Log to monitoring service if available
    if (window.errorReporter) {
      window.errorReporter.log({
        error: error.toString(),
        errorInfo,
        component: 'MCPErrorBoundary'
      });
    }
  }
  
  render() {
    if (this.state.hasError) {
      return (
        <div className="p-6 bg-red-50 border border-red-200 rounded-lg">
          <h3 className="font-semibold text-red-800 mb-2">MCP Feature Unavailable</h3>
          <p className="text-red-600">
            This feature is temporarily unavailable. The app will continue with limited functionality.
          </p>
          <button
            onClick={() => this.setState({ hasError: false })}
            className="mt-4 px-4 py-2 bg-red-600 text-white rounded"
          >
            Try Again
          </button>
        </div>
      );
    }
    
    return this.props.children;
  }
}

// Usage
<MCPErrorBoundary>
  <MCPFeatureComponent />
</MCPErrorBoundary>
```

### Fallback Strategies:

| Scenario | Fallback Approach | Implementation |
|----------|-------------------|----------------|
| Search MCP unavailable | Use cached/static examples | `SimulatedSearch` component |
| UI component fetch fails | Build custom component | `CustomUIBuilder` |
| Docs MCP unavailable | Link to external documentation | `ExternalDocsLink` |
| Logo search fails | Use placeholder or text | `LogoFallback` |
| Code reasoning fails | Use standard patterns | Never - it's MANDATORY |

### Simulated MCP Responses
```javascript
// Simulated features for when MCPs are unavailable
const SimulatedMCPResponses = {
  // Simulated search results
  search: async (query) => {
    await simulateDelay(1000);
    return {
      results: [
        {
          title: `Sample result for "${query}"`,
          content: 'This is simulated content for demonstration.',
          url: '#',
          relevance: 0.9
        },
        {
          title: `Another result about ${query}`,
          content: 'Additional simulated content to show functionality.',
          url: '#',
          relevance: 0.8
        }
      ],
      answer: `This is a simulated answer about ${query}. In production, real search results would appear here.`,
      message: 'Using simulated results (search temporarily unavailable)'
    };
  },
  
  // Simulated documentation
  docs: async (library) => {
    await simulateDelay(800);
    
    const mockDocs = {
      react: {
        content: '# React Documentation\n\n## Hooks\n\n### useState\n\n```javascript\nconst [state, setState] = useState(initialValue);\n```',
        examples: ['const [count, setCount] = useState(0);']
      },
      lodash: {
        content: '# Lodash Documentation\n\n## Array Methods\n\n### _.chunk\n\nCreates an array of elements split into groups.',
        examples: ['_.chunk([1, 2, 3, 4], 2); // => [[1, 2], [3, 4]]']
      }
    };
    
    return {
      library,
      content: mockDocs[library]?.content || `# ${library} Documentation\n\nSimulated documentation content.`,
      examples: mockDocs[library]?.examples || ['// Example code here'],
      message: 'Using simulated docs (Context7 unavailable)'
    };
  },
  
  // Simulated UI components
  uiComponent: async (type) => {
    await simulateDelay(500);
    
    const mockComponents = {
      'button': {
        code: `const Button = ({ children, variant = 'primary', onClick }) => (
          <button 
            onClick={onClick}
            className={\`px-4 py-2 rounded-lg font-medium transition-colors \${
              variant === 'primary' ? 'bg-blue-500 text-white hover:bg-blue-600' : 'bg-gray-200 hover:bg-gray-300'
            }\`}
          >
            {children}
          </button>
        );`,
        styles: 'Modern button with hover effects'
      },
      'card': {
        code: `const Card = ({ title, children }) => (
          <div className="bg-white rounded-xl shadow-lg p-6">
            <h3 className="text-xl font-semibold mb-4">{title}</h3>
            {children}
          </div>
        );`,
        styles: 'Clean card with shadow'
      }
    };
    
    return {
      component: mockComponents[type]?.code || `<div className="p-4 border rounded">Simulated ${type} Component</div>`,
      styles: mockComponents[type]?.styles || 'border-gray-300 bg-gray-50',
      message: 'Using simulated component (21st-dev unavailable)'
    };
  }
};

// Helper to simulate network delay
const simulateDelay = (ms) => new Promise(resolve => setTimeout(resolve, ms));

// Usage in components
const MCPWithSimulation = () => {
  const [data, setData] = useState(null);
  const [isSimulated, setIsSimulated] = useState(false);
  const [loading, setLoading] = useState(false);
  
  const fetchData = async () => {
    setLoading(true);
    
    try {
      // Try real MCP first
      const result = await realMCPCall();
      setData(result);
      setIsSimulated(false);
    } catch (err) {
      // Fall back to simulation
      console.warn('MCP unavailable, using simulation');
      setIsSimulated(true);
      const simulated = await SimulatedMCPResponses.search('example query');
      setData(simulated);
    } finally {
      setLoading(false);
    }
  };
  
  return (
    <div>
      {isSimulated && (
        <div className="bg-yellow-50 border border-yellow-200 p-3 rounded-lg mb-4">
          <p className="text-sm text-yellow-800">
            ⚠️ Using simulated data (MCP temporarily unavailable)
          </p>
        </div>
      )}
      {loading && <SkeletonLoader />}
      {data && <DisplayResults data={data} />}
    </div>
  );
};
```

---

## 🚀 9. PERFORMANCE & STATE MANAGEMENT

### MCP Call Optimization:
```javascript
// Optimized MCP usage with caching and batching
const OptimizedMCPManager = () => {
  // Session-only cache (no localStorage)
  const [cache] = useState(new Map());
  const [pendingRequests] = useState(new Map());
  
  // Rate limit tracking
  const [rateLimits] = useState({
    search: { count: 0, resetTime: Date.now() + 60000 },
    docs: { count: 0, resetTime: Date.now() + 60000 }
  });
  
  // Check rate limits
  const checkRateLimit = (mcpType) => {
    const limit = rateLimits[mcpType];
    if (!limit) return true;
    
    // Reset if time passed
    if (Date.now() > limit.resetTime) {
      limit.count = 0;
      limit.resetTime = Date.now() + 60000;
    }
    
    // Check if under limit (10 per minute)
    if (limit.count >= 10) {
      throw new Error(`Rate limit exceeded for ${mcpType}`);
    }
    
    limit.count++;
    return true;
  };
  
  // Batch related MCP calls
  const batchMCPCalls = async (calls) => {
    const results = await Promise.allSettled(calls);
    
    return results.map((result, index) => ({
      success: result.status === 'fulfilled',
      data: result.value || null,
      error: result.reason || null,
      index
    }));
  };
  
  // Cache with TTL
  const cachedCall = async (key, mcpCall, ttl = 300000) => { // 5 min default
    const cached = cache.get(key);
    
    if (cached && Date.now() - cached.timestamp < ttl) {
      return cached.data;
    }
    
    // Deduplicate concurrent requests
    if (pendingRequests.has(key)) {
      return pendingRequests.get(key);
    }
    
    const promise = mcpCall();
    pendingRequests.set(key, promise);
    
    try {
      const result = await promise;
      cache.set(key, { data: result, timestamp: Date.now() });
      return result;
    } finally {
      pendingRequests.delete(key);
    }
  };
  
  // Clean cache periodically
  useEffect(() => {
    const cleanup = setInterval(() => {
      const now = Date.now();
      for (const [key, value] of cache.entries()) {
        if (now - value.timestamp > 3600000) { // 1 hour
          cache.delete(key);
        }
      }
    }, 60000); // Every minute
    
    return () => clearInterval(cleanup);
  }, []);
  
  return { batchMCPCalls, cachedCall, checkRateLimit };
};
```

### Session State Best Practices:
```javascript
// Session-only state management patterns
const MCPSessionManager = () => {
  // Use React state for all storage
  const [sessionData, setSessionData] = useState({
    searches: [],
    docs: new Map(),
    components: [],
    userPreferences: {},
    mcpCalls: []
  });
  
  // Track session metrics
  const [sessionMetrics, setSessionMetrics] = useState({
    startTime: Date.now(),
    mcpCallCount: 0,
    cacheHits: 0,
    errors: [],
    performance: {
      avgResponseTime: 0,
      slowestCall: null
    }
  });
  
  // Session state hooks
  const useSessionSearch = () => {
    const addSearch = (query, results) => {
      setSessionData(prev => ({
        ...prev,
        searches: [...prev.searches, { 
          query, 
          results, 
          timestamp: Date.now() 
        }].slice(-50) // Keep last 50 searches
      }));
      
      // Update metrics
      setSessionMetrics(prev => ({
        ...prev,
        mcpCallCount: prev.mcpCallCount + 1
      }));
    };
    
    const getRecentSearches = () => sessionData.searches.slice(-10);
    
    const getSearchHistory = () => sessionData.searches;
    
    return { addSearch, getRecentSearches, getSearchHistory };
  };
  
  // Performance tracking
  const trackMCPCall = (mcpType, duration, success) => {
    setSessionMetrics(prev => {
      const newCount = prev.mcpCallCount + 1;
      const totalTime = prev.performance.avgResponseTime * prev.mcpCallCount + duration;
      const avgTime = totalTime / newCount;
      
      return {
        ...prev,
        mcpCallCount: newCount,
        performance: {
          avgResponseTime: avgTime,
          slowestCall: duration > (prev.performance.slowestCall?.duration || 0)
            ? { type: mcpType, duration }
            : prev.performance.slowestCall
        }
      };
    });
  };
  
  // Memory management
  useEffect(() => {
    // Clean old data periodically
    const cleanup = setInterval(() => {
      setSessionData(prev => {
        const cutoff = Date.now() - 3600000; // 1 hour
        return {
          ...prev,
          searches: prev.searches.filter(s => s.timestamp > cutoff),
          mcpCalls: prev.mcpCalls.filter(c => c.timestamp > cutoff)
        };
      });
    }, 60000); // Every minute
    
    return () => clearInterval(cleanup);
  }, []);
  
  return { 
    sessionData, 
    sessionMetrics, 
    useSessionSearch,
    trackMCPCall
  };
};
```

### Performance Patterns:
```javascript
// React performance optimizations for MCP results
const MCPResultsDisplay = ({ results }) => {
  const scrollRef = useRef(null);
  
  // Memoize expensive transformations
  const processedResults = useMemo(() => 
    processResults(results),
    [results]
  );
  
  // Virtual scrolling for large result sets
  const VirtualList = ({ items, itemHeight = 100 }) => {
    const [scrollTop, setScrollTop] = useState(0);
    const containerHeight = 600;
    
    const startIndex = Math.floor(scrollTop / itemHeight);
    const endIndex = Math.ceil((scrollTop + containerHeight) / itemHeight);
    const visibleItems = items.slice(startIndex, endIndex + 1);
    
    return (
      <div 
        className="overflow-auto"
        style={{ height: containerHeight }}
        onScroll={(e) => setScrollTop(e.target.scrollTop)}
      >
        <div style={{ height: items.length * itemHeight }}>
          <div style={{ transform: `translateY(${startIndex * itemHeight}px)` }}>
            {visibleItems.map((item, index) => (
              <div key={startIndex + index} style={{ height: itemHeight }}>
                <ResultItem data={item} />
              </div>
            ))}
          </div>
        </div>
      </div>
    );
  };
  
  // Lazy load heavy components
  const LazyHeavyComponent = React.lazy(() => 
    new Promise(resolve => {
      setTimeout(() => resolve(import('./HeavyComponent')), 100);
    })
  );
  
  return (
    <div ref={scrollRef} className="h-full overflow-auto">
      {processedResults.length > 50 ? (
        <VirtualList items={processedResults} />
      ) : (
        processedResults.map((item, index) => (
          <ResultItem key={index} data={item} />
        ))
      )}
      
      <React.Suspense fallback={<SkeletonLoader />}>
        <LazyHeavyComponent />
      </React.Suspense>
    </div>
  );
};

// Optimized result item with memo
const ResultItem = React.memo(({ data }) => {
  return (
    <div className="p-4 border-b hover:bg-gray-50">
      <h4 className="font-semibold">{data.title}</h4>
      <p className="text-gray-600">{data.content}</p>
    </div>
  );
}, (prevProps, nextProps) => {
  // Custom comparison for optimization
  return prevProps.data.id === nextProps.data.id &&
         prevProps.data.updated === nextProps.data.updated;
});
```

---

## 🧪 10. TESTING MCP INTEGRATION

### Pre-Build Checklist (from main system):
- [ ] Mode identified (which of the 4 modes fits best?)
- [ ] Features clear (which shortcuts did user request?)
- [ ] Code reasoning planned (MANDATORY)
- [ ] MCP availability checked
- [ ] Fallback strategies ready
- [ ] Error boundaries in place

### Testing Checklist:
- [ ] Code reasoning used for optimization (MANDATORY)
- [ ] App works without MCP features (graceful degradation)
- [ ] MCP results display correctly when available
- [ ] Error states handled for MCP failures
- [ ] Loading states during MCP calls
- [ ] Cache prevents redundant calls
- [ ] Timeouts prevent hanging
- [ ] Session state persists during use
- [ ] Memory cleaned up properly
- [ ] Download/clipboard features work
- [ ] Rate limits respected
- [ ] Performance acceptable with large datasets

### Test Scenarios:
1. **Happy path** - All MCPs available and fast
2. **Degraded** - Some MCPs unavailable
3. **Offline** - No MCP access
4. **Slow network** - Long MCP response times
5. **Mixed results** - Some succeed, some fail
6. **Rate limited** - MCPs return rate limit errors
7. **Large results** - MCPs return extensive data
8. **Concurrent calls** - Multiple MCPs called simultaneously

### Debug Pattern:
```javascript
const DebugMCPIntegration = () => {
  const [mcpStatus, setMCPStatus] = useState({});
  const [callLog, setCallLog] = useState([]);
  const [showDebug, setShowDebug] = useState(false);
  
  // Wrap MCP calls for debugging
  const debugMCPCall = async (mcpName, mcpFunction, ...args) => {
    const startTime = Date.now();
    const callId = `${mcpName}-${startTime}`;
    
    setCallLog(prev => [...prev.slice(-50), {
      id: callId,
      mcp: mcpName,
      args: args.map(a => JSON.stringify(a).slice(0, 100)),
      startTime,
      status: 'pending'
    }]);
    
    try {
      const result = await mcpFunction(...args);
      const duration = Date.now() - startTime;
      
      setCallLog(prev => prev.map(log => 
        log.id === callId 
          ? { 
              ...log, 
              status: 'success', 
              duration, 
              resultSize: JSON.stringify(result).length,
              resultPreview: JSON.stringify(result).slice(0, 100)
            }
          : log
      ));
      
      setMCPStatus(prev => ({
        ...prev,
        [mcpName]: { 
          available: true, 
          lastSuccess: Date.now(),
          avgDuration: (prev[mcpName]?.avgDuration || 0) * 0.9 + duration * 0.1
        }
      }));
      
      return result;
    } catch (error) {
      const duration = Date.now() - startTime;
      
      setCallLog(prev => prev.map(log => 
        log.id === callId 
          ? { 
              ...log, 
              status: 'error', 
              duration, 
              error: error.message 
            }
          : log
      ));
      
      setMCPStatus(prev => ({
        ...prev,
        [mcpName]: { 
          available: false, 
          lastError: Date.now(), 
          error: error.message 
        }
      }));
      
      throw error;
    }
  };
  
  // Debug panel component
  const DebugPanel = () => {
    if (!showDebug) {
      return (
        <button
          onClick={() => setShowDebug(true)}
          className="fixed bottom-4 right-4 bg-gray-800 text-white p-2 rounded-lg shadow-lg"
        >
          🐛 Debug
        </button>
      );
    }
    
    return (
      <div className="fixed bottom-0 right-0 bg-black text-white p-4 max-w-md max-h-96 overflow-auto text-xs rounded-tl-lg shadow-xl">
        <div className="flex justify-between items-center mb-2">
          <h4 className="font-bold">MCP Debug Panel</h4>
          <button onClick={() => setShowDebug(false)} className="text-gray-400 hover:text-white">
            ✕
          </button>
        </div>
        
        <div className="space-y-2">
          <div>
            <h5 className="font-semibold mb-1">MCP Status</h5>
            {Object.entries(mcpStatus).map(([mcp, status]) => (
              <div key={mcp} className={`flex justify-between ${
                status.available ? 'text-green-400' : 'text-red-400'
              }`}>
                <span>{mcp}:</span>
                <span>
                  {status.available ? `✓ ${Math.round(status.avgDuration)}ms avg` : `✗ ${status.error}`}
                </span>
              </div>
            ))}
          </div>
          
          <details className="mt-2">
            <summary className="cursor-pointer">Call Log ({callLog.length})</summary>
            <div className="mt-2 space-y-1 max-h-48 overflow-y-auto">
              {callLog.slice(-20).reverse().map(log => (
                <div key={log.id} className={`p-1 rounded text-xs ${
                  log.status === 'pending' ? 'bg-yellow-900' :
                  log.status === 'success' ? 'bg-green-900' :
                  'bg-red-900'
                }`}>
                  <div className="flex justify-between">
                    <span>{log.mcp}</span>
                    <span>{log.duration ? `${log.duration}ms` : 'pending'}</span>
                  </div>
                  {log.error && <div className="text-red-300">{log.error}</div>}
                </div>
              ))}
            </div>
          </details>
          
          <button
            onClick={() => setCallLog([])}
            className="text-xs bg-gray-700 px-2 py-1 rounded hover:bg-gray-600"
          >
            Clear Log
          </button>
        </div>
      </div>
    );
  };
  
  return { debugMCPCall, DebugPanel };
};

// Usage
const App = () => {
  const { debugMCPCall, DebugPanel } = DebugMCPIntegration();
  
  const searchWithDebug = async (query) => {
    return debugMCPCall('search', tavily.search, {
      query,
      options: { maxResults: 5 }
    });
  };
  
  return (
    <>
      {/* Your app content */}
      <DebugPanel />
    </>
  );
};
```

---

## 🗂️ 11. SINGLE-FILE ORGANIZATION WITH MCPS

### Organizing Large Apps with MCP Integration

When building large single-file apps with multiple MCP integrations, follow this structure:

```javascript
/**
 * App: Advanced MCP Integration Demo | v2.0.0 | Mode: $orchestrate + $search + $docs + $21
 * Desc: Demonstrates all MCP patterns in a single organized file
 * Features: Multi-agent system, web search, documentation, premium UI
 * Usage: Complete example of MCP integration patterns
 */

// ============================================
// IMPORTS & CONSTANTS
// ============================================
import React, { useState, useEffect, useRef, useMemo, useCallback } from 'react';
import { Search, FileText, Users, Sparkles, Download, Copy, AlertCircle, CheckCircle } from 'lucide-react';
import { LineChart, Line, XAxis, YAxis, CartesianGrid, Tooltip, ResponsiveContainer } from 'recharts';
import _ from 'lodash';
import Papa from 'papaparse';

// ============================================
// MCP CONFIGURATION & HELPERS
// ============================================
const MCPConfig = {
  search: {
    provider: 'tavily',
    fallback: 'brave',
    maxResults: 10,
    timeout: 5000,
    rateLimit: { calls: 10, window: 60000 }
  },
  docs: {
    provider: 'context7',
    maxTokens: 10000,
    cacheTTL: 3600000 // 1 hour
  },
  ui: {
    provider: '21st-dev',
    fallbackToCustom: true
  }
};

// MCP Error Handler with exponential backoff
const MCPErrorHandler = {
  // Full implementation from section 4
  async withFallback(mcpCall, fallbackFn, options = {}) {
    // ... implementation
  }
};

// ============================================
// CLAUDE API INTEGRATION
// ============================================
const claudeAPI = {
  async call(prompt, options = {}) {
    // Implementation from Examples & Patterns
    const { maxRetries = 3, timeout = 30000 } = options;
    // ... full implementation with retry logic
  }
};

// ============================================
// SESSION STATE MANAGEMENT
// ============================================
const useSessionState = () => {
  const [session] = useState({
    id: Math.random().toString(36).substr(2, 9),
    startTime: Date.now(),
    cache: new Map(),
    history: []
  });
  
  const addToHistory = useCallback((action) => {
    session.history.push({
      action,
      timestamp: Date.now()
    });
    
    // Keep only last 100 actions
    if (session.history.length > 100) {
      session.history = session.history.slice(-100);
    }
  }, [session]);
  
  return { session, addToHistory };
};

// ============================================
// MCP INTEGRATION HOOKS
// ============================================
const useMCPSearch = () => {
  const [searchCache] = useState(new Map());
  const [searching, setSearching] = useState(false);
  
  const search = async (query, options = {}) => {
    // Check cache first
    const cacheKey = `${query}-${JSON.stringify(options)}`;
    if (searchCache.has(cacheKey)) {
      return searchCache.get(cacheKey);
    }
    
    setSearching(true);
    try {
      const results = await MCPErrorHandler.withFallback(
        async () => await tavily.search({ query, options }),
        async () => await SimulatedMCPResponses.search(query)
      );
      
      searchCache.set(cacheKey, results);
      return results;
    } finally {
      setSearching(false);
    }
  };
  
  return { search, searching };
};

const useMCPDocs = () => {
  const [docsCache] = useState(new Map());
  const [loading, setLoading] = useState(false);
  
  const fetchDocs = async (library, topic = '') => {
    const cacheKey = `${library}-${topic}`;
    if (docsCache.has(cacheKey)) {
      return docsCache.get(cacheKey);
    }
    
    setLoading(true);
    try {
      const docs = await MCPErrorHandler.withFallback(
        async () => {
          const resolved = await context7.resolveLibraryId({ libraryName: library });
          return await context7.getLibraryDocs({
            context7CompatibleLibraryID: resolved[0].id,
            tokens: 10000,
            topic
          });
        },
        async () => await SimulatedMCPResponses.docs(library)
      );
      
      docsCache.set(cacheKey, docs);
      return docs;
    } finally {
      setLoading(false);
    }
  };
  
  return { fetchDocs, loading };
};

const useMCPComponents = () => {
  const [components, setComponents] = useState([]);
  const [loading, setLoading] = useState(false);
  
  const loadComponent = async (componentSpec) => {
    setLoading(true);
    try {
      const component = await MCPErrorHandler.withFallback(
        async () => await magic21st.componentBuilder(componentSpec),
        async () => buildCustomComponent(componentSpec)
      );
      
      setComponents(prev => [...prev, component]);
      return component;
    } finally {
      setLoading(false);
    }
  };
  
  return { components, loadComponent, loading };
};

// ============================================
// FEATURE MODULES
// ============================================
const SearchModule = {
  processResults: (results) => {
    return {
      summary: results.answer || 'No summary available',
      sources: results.results.map(r => ({
        title: r.title,
        url: r.url,
        snippet: r.content || r.description
      })),
      totalResults: results.results.length
    };
  },
  
  renderResults: (results) => {
    return (
      <div className="space-y-4">
        {results.summary && (
          <div className="bg-blue-50 p-4 rounded-lg">
            <h4 className="font-semibold mb-2">Summary</h4>
            <p>{results.summary}</p>
          </div>
        )}
        
        <div className="space-y-3">
          {results.sources.map((source, i) => (
            <div key={i} className="bg-white p-4 rounded-lg shadow">
              <a href={source.url} className="font-medium text-blue-600 hover:underline">
                {source.title}
              </a>
              <p className="text-gray-600 mt-1">{source.snippet}</p>
            </div>
          ))}
        </div>
      </div>
    );
  }
};

const DocsModule = {
  parseDocumentation: (docs) => {
    return {
      overview: docs.content?.slice(0, 500),
      examples: extractCodeExamples(docs),
      sections: parseSections(docs)
    };
  },
  
  renderDocumentation: (docs) => {
    return (
      <div className="prose max-w-none">
        <div dangerouslySetInnerHTML={{ __html: docs.content }} />
      </div>
    );
  }
};

const UIModule = {
  componentRegistry: new Map(),
  
  registerComponent: (name, component) => {
    UIModule.componentRegistry.set(name, component);
  },
  
  renderComponent: (componentData) => {
    const Component = UIModule.componentRegistry.get(componentData.name);
    if (Component) {
      return <Component {...componentData.props} />;
    }
    
    // Fallback to dynamic component
    return <div dangerouslySetInnerHTML={{ __html: componentData.html }} />;
  }
};

// ============================================
// SUB-COMPONENTS
// ============================================
const SearchInterface = ({ onSearch, results, searching }) => {
  const [query, setQuery] = useState('');
  
  const handleSearch = () => {
    if (query.trim()) {
      onSearch(query);
    }
  };
  
  return (
    <div className="space-y-4">
      <div className="flex gap-2">
        <input
          type="text"
          value={query}
          onChange={(e) => setQuery(e.target.value)}
          onKeyPress={(e) => e.key === 'Enter' && handleSearch()}
          placeholder="Search for current information..."
          className="flex-1 px-4 py-2 border rounded-lg"
          disabled={searching}
        />
        <button
          onClick={handleSearch}
          disabled={searching || !query.trim()}
          className="px-4 py-2 bg-blue-500 text-white rounded-lg disabled:opacity-50"
        >
          {searching ? 'Searching...' : 'Search'}
        </button>
      </div>
      
      {results && SearchModule.renderResults(results)}
    </div>
  );
};

const DocumentationViewer = ({ docs, loading }) => {
  if (loading) {
    return <SkeletonLoader variant="text" />;
  }
  
  if (!docs) {
    return <p className="text-gray-500">No documentation loaded</p>;
  }
  
  return DocsModule.renderDocumentation(docs);
};

const PremiumUIShowcase = ({ components }) => {
  return (
    <div className="grid grid-cols-1 md:grid-cols-2 gap-4">
      {components.map((component, i) => (
        <div key={i} className="bg-white p-4 rounded-lg shadow">
          {UIModule.renderComponent(component)}
        </div>
      ))}
    </div>
  );
};

// ============================================
// MAIN APP COMPONENT
// ============================================
export default function MCPIntegrationDemo() {
  // Code reasoning optimization (MANDATORY)
  useEffect(() => {
    // Initial optimization pass
    codeReasoning({
      thought: "Optimizing MCP integration architecture for multi-feature app",
      thoughtNumber: 1,
      totalThoughts: 3,
      nextThoughtNeeded: true
    });
  }, []);
  
  // Core state management
  const { session, addToHistory } = useSessionState();
  const { search, searching } = useMCPSearch();
  const { fetchDocs, loading: docsLoading } = useMCPDocs();
  const { components, loadComponent, loading: uiLoading } = useMCPComponents();
  
  // App state
  const [searchResults, setSearchResults] = useState(null);
  const [currentDocs, setCurrentDocs] = useState(null);
  const [activeTab, setActiveTab] = useState('search');
  
  // Search handler
  const handleSearch = async (query) => {
    addToHistory({ type: 'search', query });
    const results = await search(query);
    setSearchResults(SearchModule.processResults(results));
  };
  
  // Documentation handler
  const handleLoadDocs = async (library) => {
    addToHistory({ type: 'loadDocs', library });
    const docs = await fetchDocs(library);
    setCurrentDocs(DocsModule.parseDocumentation(docs));
  };
  
  // UI component handler
  const handleLoadComponent = async (type) => {
    addToHistory({ type: 'loadComponent', type });
    await loadComponent({
      searchQuery: type,
      message: `Create a ${type} component`,
      standaloneRequestQuery: `Modern ${type} with animations`
    });
  };
  
  // Render organized UI
  return (
    <div className="min-h-screen bg-gray-50">
      {/* Header */}
      <header className="bg-white shadow">
        <div className="max-w-7xl mx-auto px-4 py-4">
          <h1 className="text-2xl font-bold">MCP Integration Demo</h1>
          <p className="text-gray-600">Session: {session.id}</p>
        </div>
      </header>
      
      {/* Navigation */}
      <nav className="bg-gray-100 border-b">
        <div className="max-w-7xl mx-auto px-4">
          <div className="flex space-x-8">
            {['search', 'docs', 'ui', 'metrics'].map(tab => (
              <button
                key={tab}
                onClick={() => setActiveTab(tab)}
                className={`py-3 px-1 border-b-2 font-medium capitalize ${
                  activeTab === tab
                    ? 'border-blue-500 text-blue-600'
                    : 'border-transparent text-gray-500 hover:text-gray-700'
                }`}
              >
                {tab}
              </button>
            ))}
          </div>
        </div>
      </nav>
      
      {/* Main Content */}
      <main className="max-w-7xl mx-auto px-4 py-8">
        {activeTab === 'search' && (
          <SearchInterface
            onSearch={handleSearch}
            results={searchResults}
            searching={searching}
          />
        )}
        
        {activeTab === 'docs' && (
          <div className="space-y-4">
            <div className="flex gap-2">
              {['react', 'lodash', 'recharts'].map(lib => (
                <button
                  key={lib}
                  onClick={() => handleLoadDocs(lib)}
                  className="px-4 py-2 bg-gray-200 rounded hover:bg-gray-300"
                >
                  Load {lib} docs
                </button>
              ))}
            </div>
            <DocumentationViewer docs={currentDocs} loading={docsLoading} />
          </div>
        )}
        
        {activeTab === 'ui' && (
          <div className="space-y-4">
            <div className="flex gap-2">
              {['button', 'card', 'form', 'table'].map(type => (
                <button
                  key={type}
                  onClick={() => handleLoadComponent(type)}
                  className="px-4 py-2 bg-purple-500 text-white rounded hover:bg-purple-600"
                >
                  Add {type}
                </button>
              ))}
            </div>
            <PremiumUIShowcase components={components} />
          </div>
        )}
        
        {activeTab === 'metrics' && (
          <SessionMetrics session={session} />
        )}
      </main>
      
      {/* Debug Panel (only in development) */}
      {process.env.NODE_ENV === 'development' && <DebugPanel />}
    </div>
  );
}

// ============================================
// ADDITIONAL COMPONENTS
// ============================================
const SessionMetrics = ({ session }) => {
  const metrics = useMemo(() => {
    const actions = session.history.reduce((acc, action) => {
      acc[action.type] = (acc[action.type] || 0) + 1;
      return acc;
    }, {});
    
    return {
      totalActions: session.history.length,
      actionBreakdown: actions,
      sessionDuration: Date.now() - session.startTime,
      cacheSize: session.cache.size
    };
  }, [session]);
  
  return (
    <div className="grid grid-cols-2 gap-4">
      <div className="bg-white p-6 rounded-lg shadow">
        <h3 className="text-lg font-semibold mb-4">Session Stats</h3>
        <dl className="space-y-2">
          <div>
            <dt className="text-gray-600">Total Actions</dt>
            <dd className="text-2xl font-bold">{metrics.totalActions}</dd>
          </div>
          <div>
            <dt className="text-gray-600">Session Duration</dt>
            <dd className="text-2xl font-bold">
              {Math.floor(metrics.sessionDuration / 60000)}m
            </dd>
          </div>
          <div>
            <dt className="text-gray-600">Cache Size</dt>
            <dd className="text-2xl font-bold">{metrics.cacheSize}</dd>
          </div>
        </dl>
      </div>
      
      <div className="bg-white p-6 rounded-lg shadow">
        <h3 className="text-lg font-semibold mb-4">Action Breakdown</h3>
        <ResponsiveContainer width="100%" height={200}>
          <BarChart data={Object.entries(metrics.actionBreakdown).map(([type, count]) => ({ type, count }))}>
            <CartesianGrid strokeDasharray="3 3" />
            <XAxis dataKey="type" />
            <YAxis />
            <Tooltip />
            <Bar dataKey="count" fill="#3B82F6" />
          </BarChart>
        </ResponsiveContainer>
      </div>
    </div>
  );
};

// ============================================
// EXPORT & DOWNLOAD UTILITIES
// ============================================
const ExportUtils = {
  downloadResults: (data, format) => {
    let content, mimeType, filename;
    
    switch (format) {
      case 'json':
        content = JSON.stringify(data, null, 2);
        mimeType = 'application/json';
        filename = `mcp-results-${Date.now()}.json`;
        break;
      case 'csv':
        content = Papa.unparse(data);
        mimeType = 'text/csv';
        filename = `mcp-results-${Date.now()}.csv`;
        break;
      case 'markdown':
        content = convertToMarkdown(data);
        mimeType = 'text/markdown';
        filename = `mcp-results-${Date.now()}.md`;
        break;
    }
    
    const blob = new Blob([content], { type: mimeType });
    const url = URL.createObjectURL(blob);
    const link = document.createElement('a');
    link.href = url;
    link.download = filename;
    link.click();
    URL.revokeObjectURL(url);
  },
  
  copyToClipboard: async (data, format = 'text') => {
    const content = format === 'json' 
      ? JSON.stringify(data, null, 2)
      : convertToPlainText(data);
    
    try {
      await navigator.clipboard.writeText(content);
      return true;
    } catch (err) {
      // Fallback
      const textarea = document.createElement('textarea');
      textarea.value = content;
      document.body.appendChild(textarea);
      textarea.select();
      const success = document.execCommand('copy');
      document.body.removeChild(textarea);
      return success;
    }
  }
};

// ============================================
// SIMULATED MCP RESPONSES
// ============================================
const SimulatedMCPResponses = {
  // Full implementation from section 8
  search: async (query) => { /* ... */ },
  docs: async (library) => { /* ... */ },
  uiComponent: async (type) => { /* ... */ }
};

// ============================================
// HELPER FUNCTIONS
// ============================================
function extractCodeExamples(docs) { /* ... */ }
function parseSections(docs) { /* ... */ }
function buildCustomComponent(spec) { /* ... */ }
function convertToMarkdown(data) { /* ... */ }
function convertToPlainText(data) { /* ... */ }
```

### Organization Best Practices:
1. **Clear section separators** with ASCII art comments
2. **Logical grouping** of related functionality
3. **Centralized MCP configuration**
4. **Modular feature organization**
5. **Reusable utility functions**
6. **Consistent naming conventions**
7. **Progressive enhancement structure**
8. **Debug tools conditionally included**
9. **Export utilities at the end**
10. **Comprehensive error handling throughout**

---

## 📋 12. QUICK REFERENCE

### 12.1 Essential Imports for MCP Apps
```javascript
// React essentials
import React, { useState, useEffect, useRef, useMemo, useCallback, useReducer } from 'react';

// Icons for UI
import { 
  Search, Loader2, AlertCircle, CheckCircle, Download, Copy,
  FileText, Users, Sparkles, X, Plus, RefreshCw
} from 'lucide-react';

// Charts (if needed)
import { LineChart, Line, BarChart, Bar, XAxis, YAxis, CartesianGrid, Tooltip } from 'recharts';

// Utilities
import _ from 'lodash';
import Papa from 'papaparse';
import * as XLSX from 'xlsx';
```

---

### 12.2 MCP Cheat Sheet

| Task | MCP Function | Fallback |
|------|--------------|----------|
| Search web | `tavily.search()` → `braveSearch.webSearch()` | Simulated results |
| Get docs | `context7.resolveLibraryId()` → `getLibraryDocs()` | External links |
| UI component | `magic21st.componentBuilder()` | Custom components |
| Get logo | `magic21st.logoSearch()` | Text placeholder |
| Optimize code | `codeReasoning()` | **MANDATORY - NO FALLBACK** |

---

### 12.3 Common Patterns Quick Copy

####  MCP with Error Handling
```javascript
const result = await MCPErrorHandler.withFallback(
  async () => await mcpCall(),
  async () => await fallbackFunction(),
  { retries: 2, showNotification: true }
);
```

#### Session State Hook
```javascript
const [data, setData, getInfo] = useMCPSessionState('key', initialValue);
```

#### Download MCP Results
```javascript
<DownloadMCPResults results={data} format="json" />
```

#### Copy to Clipboard
```javascript
<CopyMCPResults results={data} format="markdown" />
```

---

*This MCP Patterns & Functions document provides comprehensive guidance for integrating Model Context Protocol features in Claude AI apps. All patterns are optimized for the artifact environment with proper error handling, fallbacks, and performance considerations.*