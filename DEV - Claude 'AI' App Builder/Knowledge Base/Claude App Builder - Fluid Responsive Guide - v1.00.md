# Claude App Builder - Fluid Responsive Design Guide

**Essential guide for implementing smooth, accessible fluid responsive design in Claude artifacts.**

## 📑 TABLE OF CONTENTS

1. [Quick Start](#1-quick-start)
2. [Core Patterns](#2-core-patterns)
3. [Implementation Rules](#3-implementation-rules)
4. [Complete Example](#4-complete-example)

---

## 1. QUICK START

### What is Fluid Design?
Smooth scaling between min/max values using CSS `clamp()`, eliminating breakpoint jumps.

### Basic Syntax
```css
clamp(MIN, PREFERRED, MAX)
```
- **MIN**: Smallest value (use rem)
- **PREFERRED**: Scaling value (rem + vw)
- **MAX**: Largest value (use rem)

### Tailwind Implementation
```jsx
// Typography
<h1 className="text-[clamp(1.5rem,1.5rem+2vw,3rem)]">

// Spacing
<div className="p-[clamp(1rem,1rem+4vw,4rem)]">

// Width
<div className="w-[clamp(20rem,50vw,60rem)]">
```

---

## 2. CORE PATTERNS

### Typography Scale
```jsx
// Consistent scale for all text sizes
const fluidText = {
  xs: "text-[clamp(0.75rem,0.7rem+0.25vw,0.875rem)]",
  sm: "text-[clamp(0.875rem,0.8rem+0.4vw,1rem)]", 
  base: "text-[clamp(1rem,0.9rem+0.5vw,1.25rem)]",
  lg: "text-[clamp(1.125rem,1rem+0.75vw,1.5rem)]",
  xl: "text-[clamp(1.5rem,1.2rem+1.5vw,2.25rem)]",
  "2xl": "text-[clamp(2rem,1.5rem+2.5vw,3rem)]",
  "3xl": "text-[clamp(2.5rem,2rem+3vw,4rem)]"
};
```

### Spacing Scale
```jsx
// Consistent spacing system
const fluidSpace = {
  xs: "clamp(0.5rem,0.4rem+0.5vw,1rem)",
  sm: "clamp(1rem,0.8rem+1vw,1.5rem)",
  md: "clamp(1.5rem,1rem+2.5vw,3rem)",
  lg: "clamp(2rem,1.5rem+2.5vw,4rem)",
  xl: "clamp(3rem,2rem+5vw,6rem)"
};

// Usage
<div className={`p-[${fluidSpace.md}] mt-[${fluidSpace.lg}]`}>
```

### Common Components
```jsx
// Fluid Container
<div className="w-[min(100%-2rem,90rem)] mx-auto px-[clamp(1rem,5vw,4rem)]">

// Fluid Grid
<div className="grid grid-cols-[repeat(auto-fit,minmax(clamp(15rem,40vw,25rem),1fr))] gap-[clamp(1rem,3vw,2rem)]">

// Fluid Button
<button className="px-[clamp(1rem,2vw,2rem)] py-[clamp(0.5rem,1vw,1rem)] text-[clamp(0.875rem,1vw,1.125rem)]">
```

---

## 3. IMPLEMENTATION RULES

### ✅ DO
- **Always use rem** for min/max (accessibility)
- **Include vw** in preferred value for scaling
- **Test zoom levels** (Ctrl/Cmd +/-)
- **Start conservative** - subtle scaling looks better
- **Use for**: Text, spacing, containers, layout widths

### ❌ DON'T
- **Avoid px** in min/max values
- **Don't use pure vw** without rem (breaks zoom)
- **Skip fluid for**: Icons, avatars, fixed UI elements
- **Don't overuse** - not everything needs to be fluid

### Accessibility Formula
```jsx
// ✅ ACCESSIBLE - Scales with viewport AND zoom
"text-[clamp(1rem,1rem+1vw,1.5rem)]"

// ❌ BROKEN - Doesn't scale with zoom
"text-[4vw]"

// ❌ INACCESSIBLE - Fixed pixels ignore user preferences
"text-[clamp(16px,4vw,24px)]"
```

### When NOT to Use Fluid
```jsx
// Fixed elements that shouldn't scale
<img className="w-12 h-12 rounded-full"> // Avatar
<svg className="w-6 h-6"> // Icon
<div className="w-64"> // Sidebar
<button className="h-10"> // Fixed height button
```

---

## 4. COMPLETE EXAMPLE

### Fluid Component Template
```jsx
const FluidCard = ({ title, description, cta }) => (
  <article className="bg-white rounded-lg shadow-lg overflow-hidden">
    {/* Fluid padding that scales with viewport */}
    <div className="p-[clamp(1rem,1rem+3vw,2rem)]">
      {/* Fluid typography hierarchy */}
      <h2 className="text-[clamp(1.25rem,1rem+1.25vw,1.75rem)] font-bold mb-[clamp(0.5rem,0.5rem+1vw,1rem)]">
        {title}
      </h2>
      
      <p className="text-[clamp(0.875rem,0.8rem+0.5vw,1.125rem)] text-gray-600 mb-[clamp(1rem,1rem+2vw,1.5rem)]">
        {description}
      </p>
      
      {/* Fluid button with consistent scaling */}
      <button className="px-[clamp(1rem,1rem+1vw,1.5rem)] py-[clamp(0.5rem,0.4rem+0.5vw,0.75rem)] bg-blue-500 text-white rounded-md text-[clamp(0.875rem,0.8rem+0.4vw,1rem)] hover:bg-blue-600 transition-colors">
        {cta}
      </button>
    </div>
  </article>
);

// Usage in fluid layout
const FluidLayout = () => (
  <main className="min-h-screen bg-gray-50 py-[clamp(2rem,2rem+4vw,6rem)]">
    <div className="w-[min(100%-2rem,90rem)] mx-auto px-[clamp(1rem,1rem+4vw,4rem)]">
      <h1 className="text-[clamp(2rem,1.5rem+2.5vw,3.5rem)] font-bold mb-[clamp(2rem,1.5rem+2.5vw,4rem)]">
        Fluid Design System
      </h1>
      
      <div className="grid grid-cols-1 md:grid-cols-2 gap-[clamp(1.5rem,1rem+2.5vw,3rem)]">
        <FluidCard 
          title="Smooth Scaling"
          description="Content scales naturally between all viewport sizes."
          cta="Learn More"
        />
        <FluidCard
          title="Better Accessibility" 
          description="Respects user zoom and font size preferences."
          cta="Get Started"
        />
      </div>
    </div>
  </main>
);
```

### Quick Formula Reference
```javascript
// Simple scaling (1rem to 1.5rem between 320px-1280px)
"clamp(1rem,1rem+0.5vw,1.5rem)"

// Aggressive scaling (1rem to 3rem)
"clamp(1rem,0.5rem+2.5vw,3rem)"

// Precise control (scale between specific viewports)
"clamp(1rem,calc(1rem+(2-1)*((100vw-20rem)/(80-20))),2rem)"
```

---

*Build smooth, accessible interfaces using fluid responsive design. Focus on readability and natural scaling across all devices.*