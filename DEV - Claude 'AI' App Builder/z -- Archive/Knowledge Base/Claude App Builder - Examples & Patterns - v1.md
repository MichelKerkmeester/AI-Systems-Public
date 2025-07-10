# Claude AI App Builder - Patterns & Examples

**Comprehensive patterns and implementations** for building AI apps in Claude artifacts.

## 📑 TABLE OF CONTENTS

### 1. [🚀 QUICK TEMPLATES](#1--quick-templates)
- Simple AI Tool
- Chat Interface
- Multi-Agent System
- Data Analyzer

### 2. [⚡ UNIVERSAL PATTERNS](#2--universal-patterns)
- 2.1 [Safe Claude API Call Pattern](#21-safe-claude-api-call-pattern)
- 2.2 [Context Management Pattern](#22-context-management-pattern)
- 2.3 [Error Handling Pattern](#23-error-handling-pattern)
- 2.4 [Loading State Pattern](#24-loading-state-pattern)

### 3. [📐 MODE-SPECIFIC PATTERNS](#3--mode-specific-patterns)
- 3.1 [$simple Mode - Complete Pattern](#31-simple-mode---complete-pattern)
- 3.2 [$chat Mode - Complete Pattern](#32-chat-mode---complete-pattern)
- 3.3 [$orchestrate Mode - Complete Pattern](#33-orchestrate-mode---complete-pattern)
- 3.4 [$analyze Mode - Complete Pattern](#34-analyze-mode---complete-pattern)

### 4. [🔧 UTILITY PATTERNS](#4--utility-patterns)
- 4.1 [File Handling](#41-file-handling)
- 4.2 [Common UI Components](#42-common-ui-components)

### 5. [📋 TESTING CHECKLIST](#5--testing-checklist)

### 6. [🎯 QUICK REFERENCE](#6--quick-reference)

---

## 1. 🚀 QUICK TEMPLATES

**What this is:** Copy-paste starting points for each app mode. These minimal templates show the core structure without extra complexity. Perfect when you need to start fast.

**Simple AI Tool:** Single-purpose generator/analyzer with immediate results
```javascript
const [input, setInput] = useState('');
const [output, setOutput] = useState(null);
const [loading, setLoading] = useState(false);
// Process → AI → Display
```


---

**Chat Interface:** Conversational AI with message history
```javascript
const [messages, setMessages] = useState([]);
const [input, setInput] = useState('');
// Send → Update History → Get Response → Display
```


---

**Multi-Agent System:** Multiple AI personalities interacting
```javascript
const [agents] = useState([...agentConfigs]);
const [conversation, setConversation] = useState([]);
// Agent Turns → Contextual Responses → Inter-agent Reactions
```


---

**Data Analyzer:** File upload + visualization + AI insights
```javascript
const [data, setData] = useState(null);
const [analysis, setAnalysis] = useState(null);
// Upload → Parse → Visualize → AI Analysis
```

---

## 2. ⚡ UNIVERSAL PATTERNS

**What this is:** Reusable code patterns that work across all app modes. These handle the common challenges you'll face in every AI app - API calls, context management, errors, and loading states. Copy these into any app as building blocks.

### 2.1 Safe Claude API Call Pattern
**Why this matters:** Claude doesn't always return perfect JSON. This pattern handles all the edge cases - prose responses, malformed JSON, and errors - so your app doesn't crash.

```javascript
const callClaude = async (prompt) => {
  try {
    const response = await window.claude.complete(prompt);
    
    // Try parsing as JSON
    try {
      return { success: true, data: JSON.parse(response) };
    } catch (e) {
      // Try extracting JSON from text
      const jsonMatch = response.match(/\{[\s\S]*\}/);
      if (jsonMatch) {
        try {
          return { success: true, data: JSON.parse(jsonMatch[0]) };
        } catch (e2) {}
      }
      
      // Fallback to text response
      return { success: true, data: { response: response } };
    }
  } catch (error) {
    return { success: false, error: error.message };
  }
};
```


---

### 2.2 Context Management Pattern
**Why this matters:** Claude has token limits. This pattern ensures you keep conversation history without hitting limits, automatically trimming old messages while preserving context.

```javascript
const ContextManager = {
  // Estimate tokens (rough approximation)
  estimateTokens: (text) => Math.ceil(text.length / 4),
  
  // Trim context to fit window
  trimContext: (messages, maxTokens = 80000) => {
    let total = 0;
    const kept = [];
    
    for (let i = messages.length - 1; i >= 0; i--) {
      const tokens = ContextManager.estimateTokens(messages[i].content);
      if (total + tokens > maxTokens) break;
      total += tokens;
      kept.unshift(messages[i]);
    }
    
    return kept;
  },
  
  // Build contextual prompt
  buildPrompt: (instruction, context = []) => {
    const trimmedContext = ContextManager.trimContext(context);
    return `
Previous context: ${JSON.stringify(trimmedContext)}

${instruction}

CRITICAL: Respond ONLY with valid JSON. No markdown, no backticks.
Format: {"response": "your response", "metadata": {}}`;
  }
};
```


---

### 2.3 Error Handling Pattern
**Why this matters:** Users need clear, actionable error messages - not technical jargon. This pattern translates Claude API errors into friendly messages and includes simple retry logic for transient failures.

```javascript
// Simple user-friendly error messages
const getErrorMessage = (error) => {
  if (error.message?.includes('rate limit')) 
    return 'Too many requests. Please wait a moment.';
  if (error.message?.includes('json')) 
    return 'Had trouble understanding the response. Trying again...';
  return 'Something went wrong. Please try again.';
};

// Basic retry logic
const retryOnce = async (fn) => {
  try {
    return await fn();
  } catch (error) {
    // One retry after 1 second
    await new Promise(r => setTimeout(r, 1000));
    return await fn();
  }
};
```


---

### 2.4 Loading State Pattern
**Why this matters:** Claude responses can take several seconds. This pattern shows dynamic loading messages that change over time, keeping users engaged instead of staring at a static spinner.

```javascript
const LoadingManager = () => {
  const [loadingStage, setLoadingStage] = useState(0);
  const stages = [
    "Processing...",
    "Thinking...",
    "Almost there...",
    "Finalizing..."
  ];
  
  useEffect(() => {
    const interval = setInterval(() => {
      setLoadingStage(prev => (prev + 1) % stages.length);
    }, 2000);
    return () => clearInterval(interval);
  }, []);
  
  return (
    <div className="flex items-center gap-2">
      <div className="animate-spin h-5 w-5 border-2 border-blue-500 border-t-transparent rounded-full" />
      <span>{stages[loadingStage]}</span>
    </div>
  );
};
```

### 2.5 Basic Input Validation
**Why this matters:** Even in a sandboxed environment, basic validation prevents errors and improves UX. These simple checks handle 90% of input issues.

```javascript
// Simple length limiting for user inputs
const validateInput = (input, maxLength = 2000) => {
  return input.trim().slice(0, maxLength);
};

// Basic check for empty or whitespace-only input
const isValidInput = (input) => {
  return input && input.trim().length > 0;
};
```

---

## 3. 📐 MODE-SPECIFIC PATTERNS

**What this is:** Complete, working examples for each of the 4 app modes. These aren't fragments - they're full implementations you can copy and run immediately. Each shows best practices for that specific type of AI app, from UI design to API integration.

### 3.1 $simple Mode - Complete Pattern
**What this builds:** A one-shot AI tool with no memory between uses. Perfect for generators, analyzers, and converters. User inputs something, Claude processes it, result displays. This example shows a business name generator - adapt it for any single-purpose tool.

```javascript
import React, { useState } from 'react';
import { Sparkles } from 'lucide-react';

export default function BusinessNameGenerator() {
  const [description, setDescription] = useState('');
  const [result, setResult] = useState(null);
  const [loading, setLoading] = useState(false);
  const [error, setError] = useState('');

  const generate = async () => {
    if (!description.trim()) return;
    
    setLoading(true);
    setError('');
    setResult(null);
    
    const prompt = `
Generate a creative business name for: "${description}"

Respond with JSON only:
{
  "name": "the business name",
  "tagline": "a catchy tagline",
  "domain": "suggested .com domain",
  "reasoning": "why this name works in 1-2 sentences"
}`;

    try {
      const response = await window.claude.complete(prompt);
      const data = JSON.parse(response);
      setResult(data);
    } catch (err) {
      setError('Failed to generate. Please try again.');
    }
    
    setLoading(false);
  };

  return (
    <div className="min-h-screen bg-gradient-to-br from-purple-50 to-blue-50 p-6">
      <div className="max-w-2xl mx-auto">
        <h1 className="text-4xl font-bold text-center mb-8">
          AI Business Name Generator
        </h1>

        <div className="bg-white rounded-xl shadow-lg p-6">
          <textarea
            value={description}
            onChange={(e) => setDescription(e.target.value)}
            placeholder="Describe your business idea..."
            className="w-full p-4 border-2 border-gray-200 rounded-lg h-32 
                     focus:border-blue-500 focus:outline-none"
            disabled={loading}
          />
          
          <button
            onClick={generate}
            disabled={loading || !description.trim()}
            className="w-full mt-4 py-3 bg-gradient-to-r from-purple-600 to-blue-600 
                     text-white rounded-lg font-semibold hover:opacity-90 
                     disabled:opacity-50 disabled:cursor-not-allowed"
          >
            {loading ? 'Generating...' : (
              <>
                <Sparkles className="inline w-5 h-5 mr-2" />
                Generate Business Name
              </>
            )}
          </button>

          {error && (
            <div className="mt-4 p-3 bg-red-100 text-red-700 rounded-lg">
              {error}
            </div>
          )}

          {result && (
            <div className="mt-6 space-y-4">
              <div className="p-6 bg-gradient-to-r from-purple-100 to-blue-100 rounded-lg">
                <h2 className="text-3xl font-bold">{result.name}</h2>
                <p className="text-gray-600 mt-2">"{result.tagline}"</p>
              </div>
              
              <div className="grid grid-cols-2 gap-4">
                <div className="p-4 bg-gray-50 rounded-lg">
                  <h3 className="font-semibold mb-1">Domain</h3>
                  <p className="text-blue-600">{result.domain}</p>
                </div>
                
                <div className="p-4 bg-gray-50 rounded-lg">
                  <h3 className="font-semibold mb-1">Why It Works</h3>
                  <p className="text-sm">{result.reasoning}</p>
                </div>
              </div>
            </div>
          )}
        </div>
      </div>
    </div>
  );
}
```


---

### 3.2 $chat Mode - Complete Pattern
**What this builds:** A conversational AI with full message history. The AI remembers everything said and responds contextually. This example shows a therapy companion - adapt it for tutors, assistants, or any ongoing conversation needs. Key feature: context management for coherent dialogue.

```javascript
import React, { useState, useRef, useEffect } from 'react';
import { Send, Bot, User } from 'lucide-react';

// Simple loading animation
const LoadingDots = () => {
  const [dots, setDots] = useState('');
  useEffect(() => {
    const interval = setInterval(() => {
      setDots(prev => prev.length >= 3 ? '' : prev + '.');
    }, 500);
    return () => clearInterval(interval);
  }, []);
  return <span>Thinking{dots}</span>;
};

export default function AITherapyCompanion() {
  const [messages, setMessages] = useState([
    {
      id: '1',
      role: 'assistant',
      content: 'Hello! I\'m here to listen and support you. How are you feeling today?'
    }
  ]);
  const [input, setInput] = useState('');
  const [loading, setLoading] = useState(false);
  const messagesEndRef = useRef(null);
  
  const scrollToBottom = () => {
    messagesEndRef.current?.scrollIntoView({ behavior: 'smooth' });
  };
  
  useEffect(() => {
    scrollToBottom();
  }, [messages]);

  const handleSend = async () => {
    if (!input.trim() || loading) return;
    
    const userMessage = {
      id: Date.now().toString(),
      role: 'user',
      content: input.trim()
    };
    
    setMessages(prev => [...prev, userMessage]);
    setInput('');
    setLoading(true);
    
    const prompt = `
You are a supportive AI therapy companion providing empathetic listening 
and gentle guidance. Be warm, understanding, and non-judgmental.

Conversation history:
${JSON.stringify(messages.slice(-10))}

User: ${userMessage.content}

Respond naturally and supportively.
Output JSON: {"response": "your supportive response"}`;

    try {
      const response = await window.claude.complete(prompt);
      const data = JSON.parse(response);
      
      setMessages(prev => [...prev, {
        id: (Date.now() + 1).toString(),
        role: 'assistant',
        content: data.response
      }]);
    } catch (err) {
      setMessages(prev => [...prev, {
        id: (Date.now() + 1).toString(),
        role: 'assistant',
        content: 'I apologize, but I had trouble responding. Please try again.'
      }]);
    }
    
    setLoading(false);
  };

  return (
    <div className="flex flex-col h-screen bg-gradient-to-b from-blue-50 to-purple-50">
      <div className="bg-white shadow-sm p-4 flex items-center gap-3">
        <Bot className="w-8 h-8 text-purple-600" />
        <div>
          <h1 className="text-xl font-semibold">Therapy Companion</h1>
          <p className="text-sm text-gray-500">A safe space to share</p>
        </div>
      </div>
      
      <div className="flex-1 overflow-y-auto p-4 space-y-4">
        {messages.map(message => (
          <div
            key={message.id}
            className={`flex gap-3 ${
              message.role === 'user' ? 'flex-row-reverse' : ''
            }`}
          >
            <div className={`w-8 h-8 rounded-full flex items-center justify-center ${
              message.role === 'user' ? 'bg-blue-500' : 'bg-purple-500'
            }`}>
              {message.role === 'user' ? 
                <User className="w-5 h-5 text-white" /> : 
                <Bot className="w-5 h-5 text-white" />
              }
            </div>
            
            <div className={`max-w-[70%] p-4 rounded-2xl ${
              message.role === 'user'
                ? 'bg-blue-500 text-white'
                : 'bg-white shadow-md'
            }`}>
              {message.content}
            </div>
          </div>
        ))}
        
        {loading && (
          <div className="flex gap-3">
            <div className="w-8 h-8 rounded-full bg-purple-500 flex items-center justify-center">
              <Bot className="w-5 h-5 text-white" />
            </div>
            <div className="bg-white shadow-md p-4 rounded-2xl">
              <LoadingDots />
            </div>
          </div>
        )}
        
        <div ref={messagesEndRef} />
      </div>
      
      <div className="bg-white border-t p-4">
        <div className="flex gap-2 max-w-4xl mx-auto">
          <input
            type="text"
            value={input}
            onChange={(e) => setInput(e.target.value)}
            onKeyPress={(e) => e.key === 'Enter' && !e.shiftKey && handleSend()}
            placeholder="Share what's on your mind..."
            className="flex-1 p-3 border-2 border-gray-200 rounded-full 
                     focus:border-purple-500 focus:outline-none"
            disabled={loading}
          />
          <button
            onClick={handleSend}
            disabled={loading || !input.trim()}
            className="p-3 bg-purple-500 text-white rounded-full hover:bg-purple-600 
                     disabled:opacity-50 disabled:cursor-not-allowed"
          >
            <Send className="w-5 h-5" />
          </button>
        </div>
      </div>
    </div>
  );
}
```


---

### 3.3 $orchestrate Mode - Complete Pattern
**What this builds:** Multiple AI agents with distinct personalities interacting together. Each agent has its own role and perspective. This example shows a startup pitch simulator with 3 investors - adapt it for debates, team discussions, or any multi-perspective scenario. Key feature: managing turn-taking and distinct voices.

```javascript
import React, { useState } from 'react';
import { Users, Play } from 'lucide-react';

export default function StartupPitchSimulator() {
  const [idea, setIdea] = useState('');
  const [simulation, setSimulation] = useState([]);
  const [running, setRunning] = useState(false);
  
  const investors = [
    { id: 'vc1', name: 'Sarah Chen', role: 'Tech VC', emoji: '👩‍💼' },
    { id: 'vc2', name: 'Marcus Johnson', role: 'Growth Investor', emoji: '👨‍💼' },
    { id: 'angel', name: 'Emma Rodriguez', role: 'Angel Investor', emoji: '👩‍🦰' }
  ];

  const runSimulation = async () => {
    if (!idea.trim() || running) return;
    
    setRunning(true);
    setSimulation([]);
    
    // Entrepreneur introduces
    setSimulation([{
      speaker: 'You',
      message: `Here's my startup idea: ${idea}`,
      emoji: '🚀'
    }]);

    // Each investor responds
    for (const investor of investors) {
      const history = simulation.map(s => `${s.speaker}: ${s.message}`).join('\n');
      
      const prompt = `
You are ${investor.name}, a ${investor.role}.

Startup pitch: "${idea}"
Previous discussion:
${history}

Ask 2-3 questions or provide feedback based on your role.
Tech VC: Focus on technology and scalability
Growth Investor: Focus on market size and metrics  
Angel Investor: Focus on vision and impact

Respond with JSON: {"feedback": "your questions/feedback"}`;

      try {
        const response = await window.claude.complete(prompt);
        const data = JSON.parse(response);
        
        setSimulation(prev => [...prev, {
          speaker: investor.name,
          message: data.feedback,
          emoji: investor.emoji,
          role: investor.role
        }]);
        
        // Brief pause between speakers
        await new Promise(resolve => setTimeout(resolve, 800));
      } catch (err) {
        console.error('Error:', err);
      }
    }
    
    setRunning(false);
  };

  return (
    <div className="min-h-screen bg-gradient-to-br from-indigo-50 to-purple-50 p-6">
      <div className="max-w-4xl mx-auto">
        <h1 className="text-4xl font-bold text-center mb-8 flex items-center justify-center gap-2">
          <Users className="w-10 h-10 text-indigo-600" />
          Startup Pitch Simulator
        </h1>

        <div className="bg-white rounded-xl shadow-xl p-6">
          <textarea
            value={idea}
            onChange={(e) => setIdea(e.target.value)}
            placeholder="Describe your startup idea in 2-3 sentences..."
            className="w-full p-4 border-2 border-gray-200 rounded-lg h-24 
                     focus:border-indigo-500 focus:outline-none"
            disabled={running}
          />
          
          <button
            onClick={runSimulation}
            disabled={running || !idea.trim()}
            className="w-full mt-4 py-3 bg-gradient-to-r from-indigo-600 to-purple-600 
                     text-white rounded-lg font-semibold hover:opacity-90 
                     disabled:opacity-50 disabled:cursor-not-allowed 
                     flex items-center justify-center gap-2"
          >
            <Play className="w-5 h-5" />
            {running ? 'Simulation Running...' : 'Start Pitch Simulation'}
          </button>

          {simulation.length > 0 && (
            <div className="mt-8 space-y-4">
              {simulation.map((entry, index) => (
                <div
                  key={index}
                  className={`p-4 rounded-lg border-l-4 ${
                    entry.speaker === 'You' 
                      ? 'bg-blue-50 border-blue-500'
                      : 'bg-indigo-50 border-indigo-500'
                  }`}
                >
                  <div className="flex items-start gap-3">
                    <span className="text-2xl">{entry.emoji}</span>
                    <div>
                      <div className="font-semibold mb-1">
                        {entry.speaker}
                        {entry.role && <span className="text-sm font-normal text-gray-500 ml-2">{entry.role}</span>}
                      </div>
                      <p className="text-gray-700">{entry.message}</p>
                    </div>
                  </div>
                </div>
              ))}
            </div>
          )}
        </div>
      </div>
    </div>
  );
}
```


---

### 3.4 $analyze Mode - Complete Pattern
**What this builds:** Data visualization combined with AI insights. Users upload files (CSV, JSON), see charts, and get AI-powered analysis. This example shows a sales analyzer - adapt it for any data analysis need. Key features: file handling, chart rendering with Recharts, and contextual AI interpretation.

```javascript
import React, { useState } from 'react';
import { LineChart, Line, BarChart, Bar, XAxis, YAxis, CartesianGrid, Tooltip, ResponsiveContainer } from 'recharts';
import { Upload, TrendingUp, FileSpreadsheet } from 'lucide-react';

export default function SalesDataAnalyzer() {
  const [data, setData] = useState(null);
  const [analysis, setAnalysis] = useState(null);
  const [loading, setLoading] = useState(false);

  const loadSampleData = async () => {
    const sampleData = [
      { month: 'Jan', sales: 45000, customers: 320 },
      { month: 'Feb', sales: 52000, customers: 385 },
      { month: 'Mar', sales: 48000, customers: 342 },
      { month: 'Apr', sales: 61000, customers: 420 },
      { month: 'May', sales: 58000, customers: 398 },
      { month: 'Jun', sales: 67000, customers: 445 }
    ];
    
    await analyzeData(sampleData);
  };

  const analyzeData = async (parsedData) => {
    setData(parsedData);
    setLoading(true);
    
    const summary = {
      totalRows: parsedData.length,
      totalSales: parsedData.reduce((sum, row) => sum + row.sales, 0),
      avgSales: parsedData.reduce((sum, row) => sum + row.sales, 0) / parsedData.length,
      sampleRows: parsedData.slice(0, 3)
    };

    const prompt = `
Analyze this sales data:
${JSON.stringify(summary, null, 2)}

Provide insights with:
1. Key trends
2. Recommendations
3. Brief forecast

Respond with JSON:
{
  "summary": "2-3 sentence executive summary",
  "trends": ["trend 1", "trend 2", "trend 3"],
  "recommendations": ["action 1", "action 2"],
  "forecast": "brief forecast"
}`;

    try {
      const response = await window.claude.complete(prompt);
      const aiAnalysis = JSON.parse(response);
      setAnalysis(aiAnalysis);
    } catch (err) {
      console.error('Analysis error:', err);
    }
    
    setLoading(false);
  };

  return (
    <div className="min-h-screen bg-gradient-to-br from-blue-50 to-indigo-50 p-6">
      <div className="max-w-6xl mx-auto">
        <h1 className="text-4xl font-bold text-center mb-8 flex items-center justify-center gap-2">
          <TrendingUp className="w-10 h-10 text-blue-600" />
          Sales Data Analyzer
        </h1>

        <div className="bg-white rounded-xl shadow-xl p-6 mb-6">
          <button
            onClick={loadSampleData}
            disabled={loading}
            className="w-full py-3 bg-blue-600 text-white rounded-lg 
                     font-semibold hover:bg-blue-700 disabled:opacity-50 
                     flex items-center justify-center gap-2"
          >
            <FileSpreadsheet className="w-5 h-5" />
            {loading ? 'Analyzing...' : 'Load Sample Data'}
          </button>
        </div>

        {data && !loading && (
          <div className="grid grid-cols-1 lg:grid-cols-2 gap-6">
            {/* Sales Chart */}
            <div className="bg-white rounded-xl shadow-xl p-6">
              <h2 className="text-xl font-semibold mb-4">Sales Trend</h2>
              <ResponsiveContainer width="100%" height={300}>
                <LineChart data={data}>
                  <CartesianGrid strokeDasharray="3 3" />
                  <XAxis dataKey="month" />
                  <YAxis />
                  <Tooltip formatter={(value) => `${value.toLocaleString()}`} />
                  <Line 
                    type="monotone" 
                    dataKey="sales" 
                    stroke="#3B82F6" 
                    strokeWidth={3}
                  />
                </LineChart>
              </ResponsiveContainer>
            </div>

            {/* Customer Chart */}
            <div className="bg-white rounded-xl shadow-xl p-6">
              <h2 className="text-xl font-semibold mb-4">Customer Growth</h2>
              <ResponsiveContainer width="100%" height={300}>
                <BarChart data={data}>
                  <CartesianGrid strokeDasharray="3 3" />
                  <XAxis dataKey="month" />
                  <YAxis />
                  <Tooltip />
                  <Bar dataKey="customers" fill="#8B5CF6" radius={[8, 8, 0, 0]} />
                </BarChart>
              </ResponsiveContainer>
            </div>

            {/* AI Analysis */}
            {analysis && (
              <div className="lg:col-span-2 bg-white rounded-xl shadow-xl p-6">
                <h2 className="text-2xl font-semibold mb-6">AI Analysis</h2>
                
                <div className="mb-6 p-4 bg-blue-50 rounded-lg">
                  <h3 className="font-semibold text-blue-900 mb-2">Summary</h3>
                  <p className="text-gray-700">{analysis.summary}</p>
                </div>
                
                <div className="grid grid-cols-1 md:grid-cols-2 gap-6">
                  <div>
                    <h3 className="font-semibold mb-3">Key Trends</h3>
                    <ul className="space-y-2">
                      {analysis.trends?.map((trend, idx) => (
                        <li key={idx} className="flex items-start">
                          <span className="text-blue-500 mr-2">•</span>
                          <span className="text-gray-700">{trend}</span>
                        </li>
                      ))}
                    </ul>
                  </div>
                  
                  <div>
                    <h3 className="font-semibold mb-3">Recommendations</h3>
                    <ul className="space-y-2">
                      {analysis.recommendations?.map((rec, idx) => (
                        <li key={idx} className="flex items-start">
                          <span className="text-green-500 mr-2">✓</span>
                          <span className="text-gray-700">{rec}</span>
                        </li>
                      ))}
                    </ul>
                  </div>
                </div>
                
                {analysis.forecast && (
                  <div className="mt-6 p-4 bg-indigo-50 rounded-lg">
                    <h3 className="font-semibold text-indigo-900 mb-2">Forecast</h3>
                    <p className="text-gray-700">{analysis.forecast}</p>
                  </div>
                )}
              </div>
            )}
          </div>
        )}
      </div>
    </div>
  );
}
```

---

## 4. 🔧 UTILITY PATTERNS

**What this is:** Helper functions and UI components you'll use repeatedly. File handling for the $analyze mode, loading animations for better UX, and other common patterns. These make your apps feel polished without reinventing the wheel.

### 4.1 File Handling
**Why this matters:** The $analyze mode needs to read uploaded files. This simple pattern handles CSVs and JSON files using Papaparse, with proper error handling. Extend it for other file types as needed.

```javascript
// Simple file reading for common formats
const readFile = async (fileName) => {
  const content = await window.fs.readFile(fileName, { encoding: 'utf8' });
  const extension = fileName.split('.').pop().toLowerCase();
  
  switch (extension) {
    case 'csv':
      // Use Papaparse for CSV
      return Papa.parse(content, { 
        header: true, 
        dynamicTyping: true,
        skipEmptyLines: true 
      }).data;
      
    case 'json':
      return JSON.parse(content);
      
    default:
      return content;
  }
};
```


---

### 4.2 Common UI Components
**Why this matters:** These small, reusable components make your app feel polished. Loading dots that animate, progress bars for file uploads, and empty states for no data. Copy these into any app for instant professional polish.

```javascript
// Animated loading dots
const LoadingDots = () => {
  const [dots, setDots] = useState('');
  
  useEffect(() => {
    const interval = setInterval(() => {
      setDots(prev => prev.length >= 3 ? '' : prev + '.');
    }, 500);
    return () => clearInterval(interval);
  }, []);
  
  return <span>Processing{dots}</span>;
};

// Simple progress bar
const Progress = ({ value, max = 100 }) => (
  <div className="w-full bg-gray-200 rounded-full h-2">
    <div 
      className="bg-blue-600 h-2 rounded-full transition-all duration-300"
      style={{ width: `${(value / max) * 100}%` }}
    />
  </div>
);

// Empty state component
const EmptyState = ({ message = "No data yet", icon: Icon = null }) => (
  <div className="text-center py-12 text-gray-500">
    {Icon && <Icon className="w-12 h-12 mx-auto mb-4 opacity-50" />}
    <p>{message}</p>
  </div>
);
```

---

## 5. 📋 TESTING CHECKLIST

**What this is:** Essential tests to run before considering your app complete. The most important: always test complex Claude prompts in the analysis tool first. This section shows you how to validate your app handles real-world usage.

### Test Your Claude Prompts First
**Critical step:** Before building your full app, always test complex prompts in the analysis tool. This saves hours of debugging by confirming Claude returns the JSON format you expect.

```javascript
// Always test complex prompts in analysis tool
const testPrompt = async () => {
  const prompt = "Your prompt here";
  
  try {
    const response = await window.claude.complete(prompt);
    console.log("Response:", response);
    
    const parsed = JSON.parse(response);
    console.log("Parsed successfully:", parsed);
  } catch (e) {
    console.error("Need to handle non-JSON response");
  }
};
```


---

### Essential Tests
**Real-world scenarios:** These tests catch the most common issues users will encounter. Run through this checklist to ensure your app handles edge cases gracefully.

- [ ] Empty input → Shows appropriate message
- [ ] Long input → Truncated appropriately  
- [ ] Rapid clicks → Prevented or handled
- [ ] Malformed JSON from Claude → Handled gracefully
- [ ] File upload errors → Clear error message

---

## 6. 🎯 QUICK REFERENCE

**What this is:** Your cheat sheet for Claude artifact development. All the available imports, common Tailwind classes, and essential patterns in one place. Keep this open while coding for quick lookups.

### Essential Imports
**What's available:** All the libraries you can use in Claude artifacts. No need to install anything - these are pre-loaded. React for UI, Lucide for icons, Recharts for data viz, and more.

```javascript
// React hooks
import React, { useState, useEffect, useRef, useReducer, useMemo, useCallback } from 'react';

// Icons
import { Send, Loader2, AlertCircle, CheckCircle, X, Plus, Search, 
         Play, Pause, Download, Upload, RefreshCw, Settings } from 'lucide-react';

// Charts  
import { LineChart, BarChart, PieChart, AreaChart, RadarChart,
         Line, Bar, Pie, Area, Radar, XAxis, YAxis, CartesianGrid, 
         Tooltip, Legend, ResponsiveContainer } from 'recharts';

// Utilities
import _ from 'lodash';
import Papa from 'papaparse';
import * as math from 'mathjs';
```


---

### CSS Classes (Tailwind)
**Pre-compiled only:** Claude artifacts use Tailwind's utility classes, but you can't create custom ones. These examples show the most common patterns for layouts, styling, and responsive design.

```javascript
// Containers
"min-h-screen max-w-4xl mx-auto p-4 sm:p-6 lg:p-8"

// Cards
"bg-white rounded-lg shadow-lg p-6"

// Buttons
"px-4 py-2 bg-blue-600 text-white rounded-lg hover:bg-blue-700 disabled:opacity-50"

// Inputs
"w-full p-3 border-2 border-gray-200 rounded-lg focus:border-blue-500 focus:outline-none"

// Animations
"transition-all duration-300 transform hover:scale-105"

// Responsive
"grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4"
```

---

*Remember: Great AI apps in Claude artifacts combine simplicity with functionality. Test your prompts, handle errors gracefully, and focus on creating delightful experiences within the artifact constraints.*