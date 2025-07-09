# Ticket Examples & Patterns

## Table of Contents

1. [🔍 MODE COMPARISON](#1-🔍-mode-comparison)
   - 1.1 [Same Request, Different Modes](#11-same-request-different-modes)
   - 1.2 [`$c` Complex Mode](#12-c-complex-mode)
2. [📝 CLARIFYING QUESTIONS](#2-📝-clarifying-questions)
   - 2.1 [When You Need More Info](#21-when-you-need-more-info)
3. [🚀 EPIC BREAKDOWN PATTERN](#3-🚀-epic-breakdown-pattern)
   - 3.1 [`$e` Epic Mode Example](#31-e-epic-mode-example)
4. [💡 SPECIAL FORMATTING CASES](#4-💡-special-formatting-cases)
   - 4.1 [When to Use Special Elements](#41-when-to-use-special-elements)
   - 4.2 [Figma Link Patterns](#42-figma-link-patterns)
   - 4.3 [Image Embedding](#43-image-embedding)
   - 4.4 [Icons in Headers](#44-icons-in-headers)
5. [🐛 BUG TICKET EXAMPLE](#5-🐛-bug-ticket-example)
   - 5.1 [`$s` Bug Ticket](#51-s-bug-ticket)
6. [🔧 IMPROVEMENT TICKET EXAMPLE](#6-🔧-improvement-ticket-example)
   - 6.1 [`$s` Improvement Ticket](#61-s-improvement-ticket)
   - 6.2 [Arrow Notation](#62-arrow-notation)
   - 6.3 [Notice Callouts](#63-notice-callouts)
   - 6.4 [Logic Sections](#64-logic-sections)
   - 6.5 [Nested Information](#65-nested-information)
7. [🎯 GOOD vs VERBOSE EXAMPLES](#7-🎯-good-vs-verbose-examples)
   - 7.1 [Example 1: Column Resizing Feature](#71-example-1-column-resizing-feature)
   - 7.2 [Example 2: User Dashboard](#72-example-2-user-dashboard)
8. [📊 PATTERN TRANSFORMATIONS](#8-📊-pattern-transformations)
   - 8.1 [Complex Features → Phased Tickets](#81-complex-features--phased-tickets)
9. [🔍 COMMON SCENARIOS](#9-🔍-common-scenarios)
   - 9.1 [Scenario: Unclear Requirements](#91-scenario-unclear-requirements)
   - 9.2 [Scenario: Bug Report](#92-scenario-bug-report)
   - 9.3 [Scenario: Performance Improvement](#93-scenario-performance-improvement)
10. [⚡ QUICK FIXES REFERENCE](#10-⚡-quick-fixes-reference)
    - 10.1 [Common Issues & Solutions](#101-common-issues--solutions)
11. [🎯 QUALITY CHECKLIST](#11-🎯-quality-checklist)
12. [💬 SAMPLE RESPONSES](#12-💬-sample-responses)
13. [📐 MODE SELECTION GUIDE](#13-📐-mode-selection-guide)

---

## 1. 🔍 MODE COMPARISON

### 1.1 Same Request, Different Modes

**Request:** "We need search filters"

---

#### 1.1.1 `$q` Quick Mode
```markdown
### Search Filters

**User Value:** Find what they need faster

**Business Goal:** Reduce bounce rate on search page

---

## Requirements
- Filter by category and date
- Show active filters
- Clear all filters option

---

## Design
- [Figma - Search Filters](link)

---

## Success Criteria
- [ ] Filters work on mobile
- [ ] Results update instantly
- [ ] Users can combine filters
```

---

#### 1.1.2 `$s` Standard Mode
```markdown
### Advanced Search Filters

**User Value:** Find relevant results faster with category and date filters

**Business Goal:** Reduce search abandonment rate (currently 67%)

---

## Requirements
- User can filter by category, date range, and status
- Filters update results without page refresh
- Selected filters remain visible and removable
- Mobile-responsive filter panel

---

## Design
- [Figma - Search Filters](link)
- Filters collapse on mobile to save space

---

## Success Criteria
- [ ] Results update within 300ms of filter change
- [ ] Users can combine multiple filters
- [ ] Filter state persists during session

---

## Dependencies
- Requires: API filter endpoint (#1234)
- Blocks: Saved searches feature (#1240)
```

---

### 1.2 `$c` Complex Mode

```markdown
### ◇ Search Experience Overhaul

---

# ⌘ About

Our search is failing users - 67% abandon without finding what they need. Competitors offer smart filtering and personalization. We need a complete overhaul to remain competitive.

**User Value:** Find exactly what they need with smart filters and suggestions

**Business Goal:** Increase search-to-conversion from 12% to 25%

---

[[*TOC*]]

---

## → Design

### Flows
- [Figma - Search Journey Complete](link)
- [Figma - Filter Interactions](link)
- [Figma - Personalization States](link)

### Components
- [Figma - Filter Components](link)
- [Figma - Search Results](link)
- [Figma - Mobile Patterns](link)

**Notice:** Design includes A/B test variations for filter placement.

---

## ❖ Phase 1: Basic Filters (Sprint 1)
- Category and date filters
- Mobile-responsive design  
- Real-time result updates
- Clear all functionality

---

## ❖ Phase 2: Smart Features (Sprint 2)
- Auto-suggestions while typing
- Popular filter combinations
- Recent search history
- Filter usage analytics

---

## ❖ Phase 3: Personalization (Sprint 3)
- Saved filter sets
- Recommended filters based on behavior
- Quick filter shortcuts
- Personalized result ranking

---

## ✓ Success Criteria
- [ ] 50% reduction in "no results" searches
- [ ] Average results found in <3 clicks  
- [ ] Search-to-conversion rate reaches 25%
- [ ] Mobile usage increases by 40%

---

## ⊗ Dependencies
- Requires: New search infrastructure (#1230)
- Requires: User behavior tracking (#1231)  
- Blocks: AI recommendations (#1250)

---

## ⚠️ Risks
- **Performance:** May need caching for <300ms response
- **Adoption:** Users attached to current search
- **Data Privacy:** Personalization requires consent
```

---

## 2. 📝 CLARIFYING QUESTIONS

### 2.1 When You Need More Info

**Vague Request:** "Make the dashboard better"

**Response:**
```
I need some clarification to write an effective ticket:

What specific problems are users having with the current dashboard?

Once I understand the pain points, I can create a focused ticket with clear success criteria.
```

---

**Missing Context:** "Add export feature"

**Response:**
```
To create a complete ticket, I need to know:

What data should users be able to export, and in what formats?

This will help me define clear requirements and success criteria.
```

---

**Too Broad:** "Redesign the whole app"

**Response:**
```
This sounds like multiple features. To keep tickets actionable, should we:

1. Start with the highest-priority area?
2. Create an epic with multiple tickets?

What would have the most impact for users right now?
```

---

## 3. 🚀 EPIC BREAKDOWN PATTERN

### 3.1 `$e` Epic Mode Example

**Request:** "Customer portal for self-service"

```markdown
### Epic: Customer Self-Service Portal

**User Value:** Customers resolve issues without waiting for support

**Business Goal:** Reduce support tickets by 40%

---

## Overview
Enable customers to manage their accounts, view data, and resolve common issues independently through a dedicated portal.

---

## Success Metrics
- [ ] 40% reduction in support tickets
- [ ] 80% of users self-serve successfully
- [ ] Average resolution time < 5 minutes

---

## Child Tickets

### Phase 1: Foundation
- [ ] **Authentication & Access** - Secure login and role management
- [ ] **Dashboard Overview** - Key account info at a glance
- [ ] **Navigation Structure** - Intuitive portal layout

### Phase 2: Core Features  
- [ ] **Account Management** - Update profile and preferences
- [ ] **Billing & Invoices** - View and download statements
- [ ] **Usage Analytics** - Track product usage

### Phase 3: Self-Service
- [ ] **Knowledge Base Integration** - Searchable help articles
- [ ] **Automated Troubleshooting** - Common issue resolution
- [ ] **Ticket Submission** - When self-service isn't enough

---

## Dependencies
- Requires: SSO infrastructure (#1200)
- Requires: API rate limiting (#1201)

---

## Timeline
12 weeks (4 weeks per phase)
```

---

## 4. 💡 SPECIAL FORMATTING CASES

### 4.1 When to Use Special Elements

Use special formatting to enhance clarity and create visual hierarchy in your tickets.

---

### 4.2 Figma Link Patterns

```markdown
## → Design

### Flows
- [Search Engine V2.0](figma-link)
- [User Journey - Search to Purchase](figma-link)

### Components  
- [Header & Filter System](figma-link)
- [Sheet Components](figma-link)
- [Data Visualization](figma-link)

### Mobile
- [iOS Responsive Views](figma-link)
- [Android Adaptations](figma-link)

**Notice:** Check component headers in Figma for implementation notes.
```

---

### 4.3 Image Embedding

When including screenshots or diagrams:
```markdown
## → Design
- [Figma - Complete Flow](link)

### Screenshots
![Search filter expanded state](attachment:12345:search-filters-expanded.png)
![Mobile responsive view](attachment:12346:search-filters-mobile.png)

**Notice:** Red annotations in screenshots indicate interaction hotspots.
```

---

### 4.4 Icons in Headers

Icons are optional but when used, maintain consistency throughout the ticket:

```markdown
### ◇ Feature Component
## ❖ Requirements
## → Design
## ✓ Success Criteria
## ⊗ Dependencies
## ⚠️ Risks & Considerations
# ⌘ About This Feature
```

---

## 5. 🐛 BUG TICKET EXAMPLE

### 5.1 `$s` Bug Ticket

```markdown
### Bug: Search Filters Reset on Back Navigation

**User Value:** Keep selected filters when navigating back to search results

**Business Goal:** Reduce user frustration and abandonment (23% drop-off rate)

---

## Current Behavior
1. User applies multiple filters
2. User clicks on a search result
3. User clicks browser back button
4. **Bug:** All filters are cleared

---

## Expected Behavior
- Filters persist when navigating back
- Selected filters remain visible
- Results show filtered state

---

## Design
- [Figma - Expected Filter State](link)
- [Video - Current Bug Behavior](link)

**Notice:** This worked correctly before v2.3 release.

---

## Success Criteria
- [ ] 100% of filters persist on back navigation
- [ ] Filter state restored within 100ms
- [ ] Works across all major browsers

---

## Dependencies
- Requires: Browser history API investigation (#1454)
- Blocks: Search analytics accuracy (#1455)
```

---

## 6. 🔧 IMPROVEMENT TICKET EXAMPLE  

### 6.1 `$s` Improvement Ticket

```markdown
### Improvement: Faster Chart Loading

**User Value:** See data instantly without waiting

**Business Goal:** Reduce dashboard bounce rate by 25%

---

## Current Performance
- Initial load: 3-5 seconds
- Subsequent loads: 2-3 seconds  
- Mobile: 5-7 seconds

---

## Target Performance
- Initial load: <1 second
- Subsequent loads: <500ms
- Mobile: <2 seconds

---

## Design
- [Figma - Loading States](link)
- [Figma - Progressive Enhancement](link)

**Notice:** Show skeleton loaders during data fetch.

---

## Requirements
- Implement progressive data loading
- Add skeleton states while loading
- Cache rendered charts for session
- Lazy load below-fold charts

---

## Success Criteria
- [ ] 90% of charts load in <1 second
- [ ] 25% reduction in bounce rate
- [ ] Performance budget: 200KB JS max

---

## Dependencies
- Requires: Performance monitoring setup (#1501)
- Requires: CDN configuration (#1502)
- Blocks: Mobile app integration (#1520)
```

---

### 6.2 Arrow Notation (`→`)

Use for cause-and-effect or user flows:
```markdown
- **Click filter** → Results update instantly
- **Hover on chart** → Show detailed tooltip
- **Save changes** → Confirmation message appears
```

---

### 6.3 Notice Callouts

For critical information that might be missed:
```markdown
## Design
- [Figma - Feature](link)

**Notice:** Component headers contain implementation notes
```

---

### 6.4 Logic Sections

When behavior has conditions:
```markdown
### Logic:
- **IF new user (<5 actions)** → Show onboarding
- **IF returning user** → Show dashboard
- **IF error occurs** → Display helpful message
```

---

### 6.5 Nested Information

For related but detailed specs:
```markdown
## Requirements
- Resizable columns
  - Default: 240px
  - Min: 120px  
  - Max: unlimited
- Persistent settings
  - Store in user preferences
  - Apply on next visit
```

---

## 7. 🎯 GOOD vs VERBOSE EXAMPLES

### 7.1 Example 1: Column Resizing Feature

---

#### 7.1.1 ❌ VERBOSE (Too Much Detail)

```markdown
### ◇ Columns | Resize Functionality Implementation

# ⌘ About
Our current data table lacks the ability for users to resize columns, which has been a frequent request in user feedback sessions. Based on analytics showing that 73% of power users struggle with fixed column widths when trying to view multiple data points simultaneously, we need to implement a comprehensive column resizing system. This will involve creating new React components, implementing drag handlers, managing state persistence, and ensuring cross-browser compatibility...

# ❖ Implementation

## ◇ Resize interaction
- **Hovering over the outer right border** of a column → The cursor changes to the **"Resize"** state
- Implement using ResizeObserver API with proper event handling
- Add event listeners for mousedown, mousemove, mouseup
- Store column widths in localStorage for persistence
- Implement minimum and maximum width constraints
- Handle edge cases for very long content...

[Technical details continue...]
```

---

#### 7.1.2 ✅ CONCISE (Focused on Outcomes)

```markdown
### Column Resizing

**User Value:** See all important data without horizontal scrolling

**Business Goal:** Increase power user retention by 15%

---

## Design

### Interactions
- [Figma - Resize States](link)
- [Figma - Cursor Behaviors](link)

### Specifications  
- [Figma - Width Constraints](link)
- [Figma - Mobile Behavior](link)

**Notice:** Min: 120px, Max: none, Default: 240px

---

## Requirements
- **Hover column edge** → Resize cursor appears
- **Drag edge** → Column resizes with blue indicator
- **Double-click edge** → Auto-fit to content
- Widths persist between sessions

---

## Success Criteria
- [ ] 100% of columns resizable (except locked)
- [ ] Resize completes in <16ms (60fps)
- [ ] Settings persist for 30+ days

---

## Dependencies
- Requires: Table component update (#4171)
- Blocks: Column pinning (#4180)
```

---

### 7.2 Example 2: User Dashboard

---

#### 7.2.1 ❌ VERBOSE (Too Many Implementation Details)
```markdown
### ◇ Platform | User Dashboard Redesign v2.0

# ⌘ About
The current dashboard has become cluttered and overwhelming based on user feedback sessions conducted in Q3. With the addition of new features over the past year, the information architecture no longer serves our users' primary needs. Heat mapping studies show users spending excessive time searching for key metrics...

# ❖ Implementation

## ◇ Dashboard Layout Grid System
### Grid Specifications:
- 12-column responsive grid
- Breakpoints: 320px, 768px, 1024px, 1440px
- Gap spacing: 16px mobile, 24px desktop
- Card components with 8px border radius...

[Extensive implementation details...]
```

---

#### 7.2.2 ✅ CONCISE (Clear and Actionable)
```markdown
### Dashboard Redesign

**User Value:** See most important metrics at a glance

**Business Goal:** Improve daily active usage by highlighting key features

---

## Requirements
- Customizable widget layout
- Key metrics visible above fold
- Drag-and-drop widget arrangement
- Quick actions for common tasks

---

## Design
- [Figma - Dashboard v2](link)
- Default layout prioritizes usage data

---

## Success Criteria
- [ ] Page loads in under 2 seconds
- [ ] Users can customize layout
- [ ] Mobile view shows essential metrics first

---

## Dependencies
- Requires: Widget API (#890)
```

---

#### 7.2.3 Another Concise Example
```markdown
### Chart Interaction Updates

**User Value:** Understand data trends at a glance with interactive charts

**Business Goal:** Increase data exploration by 40%

---

## Requirements
- **Donut charts** → Show 1 decimal value (not 2)
- **Tree maps** → Remove 3rd layer, disable 2nd layer except "Others"
- **Tooltips** → Display on hover with updated styling
- Consistent color tokens across all charts

---

## Design
- [Figma - Data Visualization v2](link)
- [Component Library](link)

---

## Success Criteria
- [ ] All charts load in <500ms
- [ ] Touch-friendly on mobile (44px minimum touch target)
- [ ] Consistent styling across Statistics, Trends, Churn pages

---

## Dependencies
- Requires: Updated color tokens (#4331)
- Blocks: Dashboard redesign (#4340)

---

**Notice:** Always check component headers in Figma for implementation notes
```

---

## 8. 📊 PATTERN TRANSFORMATIONS

### 8.1 Complex Features → Phased Tickets

Instead of one massive ticket, break into phases with clear boundaries:

---

#### 8.1.1 Phase-Based Ticket Example

```markdown
### Feed Personalization System

**User Value:** See the most relevant content first, every time

**Business Goal:** Increase daily active users by 30%

---

## Phase 1: Data Collection (Week 1-2)
- Track user interactions with feed items
- Store preference signals
- Basic analytics dashboard

---

## Phase 2: Algorithm Implementation (Week 3-4)
- Personalization engine based on behavior
- A/B test framework
- Fallback to default feed

---

## Phase 3: Optimization (Week 5-6)
- Machine learning improvements
- Real-time adjustments
- Performance tuning

---

## Success Criteria
- [ ] 30% increase in session duration
- [ ] 50% more interactions per session
- [ ] <100ms added latency

---

## Design
- [Figma - Personalized Feed](link)
- [Algorithm Documentation](link)

---

## Dependencies
- Requires: User tracking infrastructure (#2001)
- Requires: A/B testing framework (#2002)
```

---

## 9. 🔍 COMMON SCENARIOS

### 9.1 Scenario: Unclear Requirements

#### Response:
```markdown
I need clarification on [specific aspect]:
- Who is the primary user for this feature?
- What problem are we solving?
- Do we have designs/mockups?
- What's the success metric?
```

---

### 9.2 Scenario: Bug Report

#### Template:
```markdown
### Bug: [Feature Name]

**User Value:** [What users can do when fixed]

**Business Goal:** [Business impact of fixing]

---

## Current Behavior
[What's happening]

---

## Expected Behavior
[What should happen]

---

## Steps to Reproduce
1. [Step one]
2. [Step two]

---

## Design
- [Screenshot of issue]
- [Expected behavior reference]

---

## Success Criteria
- [ ] [Measurable outcome]
```

---

### 9.3 Scenario: Performance Improvement

#### Template:
```markdown
### Improvement: [Feature] Performance

**User Value:** [Feature] loads 3x faster

**Business Goal:** [Business metric improvement]

---

## Current Performance
- Metric: [current value]

---

## Target Performance
- Metric: [target value]

---

## Requirements
- Optimize [specific area]
- Maintain current functionality
- Track performance metrics

---

## Success Criteria
- [ ] Page load under 2 seconds
- [ ] No feature regression
- [ ] Performance monitoring in place
```

---

## 10. ⚡ QUICK FIXES REFERENCE

### 10.1 Common Issues & Solutions

| If ticket is... | Do this... | Example |
|-----------------|------------|---------|
| Too technical | Replace with user language | "Implement OAuth2" → "Secure login with Google/Microsoft" |
| Too vague | Add specific outcomes | "Improve performance" → "Page loads in under 2 seconds" |
| Too long | Focus on essential sections | Remove background, keep user value and requirements |
| Missing why | Add user value statement | Start with "Users can..." or "This helps users..." |
| Over-specified | Remove implementation details | "Using React hooks" → "Interactive form" |
| No success criteria | Add measurable outcomes | "It works" → "95% form completion rate" |
| Missing dividers | Add `---` between sections | Every section needs visual separation |
| No emphasis | Add **bold** to key terms | Highlight important concepts |

---

## 11. 🎯 QUALITY CHECKLIST

Before delivering any ticket, verify:

- [ ] Has `---` dividers between all sections?
- [ ] Can be read in under 2 minutes?
- [ ] Clear user value in first section?
- [ ] Requirements are outcomes, not solutions?
- [ ] Success criteria are measurable?
- [ ] Links to designs (not descriptions)?
- [ ] Dependencies noted if any (with ticket numbers)?
- [ ] Proper formatting with **bold** emphasis?
- [ ] Would a developer know what "done" looks like?
- [ ] Is this one deployable unit?

If any answer is "no," revise before delivering.

---

## 12. 💬 SAMPLE RESPONSES

---

### 12.1 When request is perfect:
"Here's your ticket, ready for sprint planning:"
[Artifact with ticket]

---

### 12.2 When clarification needed:
"I need one detail to complete this ticket: [specific question]"

---

### 12.3 When suggesting split:
"This sounds like 3 separate features. Would you like:
1. One epic with child tickets?
2. Just the highest priority feature?
3. All three as separate tickets?"

---

### 12.4 When design missing:
"I've created the ticket structure. Note that we'll need design mockups before development can start:"
[Artifact with ticket marked "**Needs:** Design mockups"]

---

## 13. 📐 MODE SELECTION GUIDE

```
How complex is the feature?
├─ Single, clear feature → $q (Quick)
├─ Standard feature with details → $s (Standard) DEFAULT
├─ Multi-part or phased → $c (Complex)
└─ Major initiative → $e (Epic)
```

Remember: When in doubt, use $s (Standard). It's the sweet spot for most tickets.