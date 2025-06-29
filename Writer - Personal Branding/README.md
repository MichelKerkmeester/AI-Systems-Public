# Personal Branding Writer - User Guide

## 🚀 What is This?

The Personal Branding Writer is a specialized Claude configuration that transforms you into a strategic marketing leader with 10+ years of experience. It helps you create authentic, data-driven marketing content that connects with audiences through human stories and actionable insights.

**Key Benefits:**
- Write marketing content with a consistent, professional voice
- Get 3 variations of every piece (concise/authentic/valuable)
- Access proven marketing frameworks (SVC, CASE, QPT, etc.)
- Create content that drives engagement and action
- Learn from a voice that balances data with humanity

⚡ Important Note: This is a basic system designed for quick personal branding content creation. To make this enterprise-ready for you personal business, you'll need to enhance it with additional knowledge base items such as:

- Brand Guidelines and Voice Documentation
- Target Audience Personas and Insights
- Product/Service Information Repositories
- Market, Industry, and Competitor Research
- Examples & Case Studies Library

.

## 🎨 PRO TIP: Make This YOUR Brand Voice!

**Transform this system into your personal or company brand voice using my [Prompt Improver](https://github.com/MichelKerkmeester/AI-Systems-Public/tree/main/Writer%20-%20Prompt%20Improver)!**

This system comes configured as "Sarah Chen" - a marketing leader with specific traits and experiences. But you can instantly customize it to match YOUR unique voice, industry, and expertise.

**Example customization prompt:**
```
$full Improve this prompt '''
Transform the Personal Branding Writer system into a [YOUR ROLE] writer for [YOUR BRAND].

Current system: Sarah Chen, marketing leader, 10+ years, data-driven storytelling
Target system: [YOUR NAME/BRAND], [YOUR ROLE], [YOUR EXPERIENCE], [YOUR VOICE TRAITS]

Keep the framework structure and 3-variation output system.
'''
```

See the full "Customization" section below for detailed instructions.

.

## 🎯 Full Customization Guide

### Transform Into ANY Brand Voice
The Personal Branding Writer system is fully customizable. While it comes configured as "Sarah Chen" (a marketing leader), you can adapt it to any role, industry, or brand voice.

**Quick customization with [Prompt Improver](https://github.com/MichelKerkmeester/AI-Systems-Public/tree/main/Writer%20-%20Prompt%20Improver):**

```
$full Improve this prompt '''
Transform the Personal Branding Writer system (currently configured as Sarah Chen, marketing leader) into a [YOUR ROLE] writer system for [YOUR COMPANY/BRAND].

Key changes needed:
- Replace Sarah Chen with [YOUR NAME/BRAND]
- Change from marketing focus to [YOUR INDUSTRY/FOCUS]
- Adjust experience from "10+ years in marketing" to [YOUR BACKGROUND]
- Modify voice characteristics from "data-driven storytelling" to [YOUR VOICE TRAITS]
- Keep the framework structure but adapt examples to [YOUR FIELD]
- Maintain the 3-variation output system
'''
```

**Example for a Technical Writer:**
```
$full Improve this prompt '''
Transform the Personal Branding Writer system into a technical documentation writer system for a developer-focused SaaS company.

Key changes:
- Replace marketing storytelling with technical clarity
- Change campaign examples to API documentation examples
- Adjust tone from "human stories" to "developer-friendly precision"
- Keep the quality frameworks but optimize for technical accuracy
'''
```

.

## 📋 Quick Setup in Claude

### Step 1: Create a New Project
1. Go to [claude.ai](https://claude.ai)
2. Click "Projects" in the sidebar
3. Click "Create project"
4. Name it "Personal Branding Writer" (or your customized version)

### Step 2: Add the System Instructions
1. In your project, click "Edit project details"
2. Find the "Custom instructions" section
3. Copy and paste the main system file: `Writer - Personal Branding - v1.0.md`
4. Save the project

### Step 3: Upload Framework Document
Upload the framework reference document to your project:
- `Copywriter Frameworks.md` (contains all writing frameworks)

### Step 4: Start Creating!
Begin any conversation in the project, and Claude will write in the configured brand voice (default: Sarah Chen), delivering marketing content in artifacts with 3 variations.

.

## 🎯 How to Use

### Basic Usage
Simply describe what you need:
```
Write a LinkedIn post about the importance of A/B testing
```

### Mode Selection
The system has six specialized modes:

| Mode | Command | Use For | Example Output Style |
|------|---------|---------|---------------------|
| **Share** | `$share` or `$s` (DEFAULT) | Knowledge & insights | "Here's what worked..." |
| **Connect** | `$connect` or `$c` | Building relationships | "Ever notice how we all..." |
| **Advise** | `$advise` or `$a` | Problem-solving | "Start with these 3 steps..." |
| **Story** | `$story` or `$st` | Case studies | "The campaign was failing until..." |
| **Update** | `$update` or `$u` | Professional news | "Excited to share our team's..." |
| **Improve** | `$improve` or `$i` | Optimize content | Full VEST evaluation + refined versions |

### Mode Examples:
```
$share insights from our email campaign

$connect with other marketers about budget constraints

$advise on improving conversion rates

$story about our product launch campaign

$update announcing our new marketing initiative

$improve [creates content then automatically refines it]
```

.

## 🎨 Tone Modifiers

### Add Tones for Different Contexts
Combine modes with tones for precise voice control:

| Tone | Code | Best For |
|------|------|----------|
| **Casual** | `+ $casual` | Social media, team updates |
| **Technical** | `+ $technical` | Data reports, analytics |
| **Educational** | `+ $educational` | Tutorials, guides |
| **Fun** | `+ $fun` | Social campaigns |
| **Formal** | `+ $formal` | Executive communications |
| **Minimal** | `+ $minimal` | Ad copy, headlines |

### Tone Combination Examples:
```
$share + $casual insights about influencer marketing

$advise + $technical on setting up GA4 conversion tracking

$connect + $fun about marketing fails we've all experienced
```

.

## ✅ Output Format

### Every Response Includes:
1. **Always in an artifact** (formatted content block)
2. **3 variations minimum:**
   - **Most concise:** Fewest words, maximum impact
   - **Most authentic:** Natural Sarah voice with stories
   - **Most valuable:** Maximum actionable takeaway
3. **Framework noted** when applicable
4. **Platform optimization** when specified

### Example Output Structure:
```
FRAMEWORK USED: SVC (Situation•Value•Connection)
PLATFORM: LinkedIn

### Most concise:
Stock photos killed our CTR. Real employees: +47%. You?

### Most authentic:
Client fought us on using employee photos vs stock. We A/B tested anyway. 
Real faces won by 47%. Sometimes "unprofessional" is exactly what people 
want. When's your last visual audit?

### Most valuable:
Marketing truth: We replaced stock photos with real employee shots. CTR 
jumped 47%, cost per lead dropped 31%. Test: Swap one hero image for 
authentic photo. Track for 2 weeks. Share results?
```

.

## 💡 Pro Tips

### 1. Specify Platform for Optimized Content
```
Write a Twitter thread about content marketing ROI

Create an Instagram caption for our new campaign launch

Draft a LinkedIn article about marketing automation
```

### 2. Use Frameworks Directly
Request specific frameworks when you know what you need:
```
Use the CASE framework to tell our product launch story

Apply QPT to challenge assumptions about email marketing

Create a PATH framework story about fixing our attribution
```

### 3. The Magic of $improve Mode
This mode automatically:
- Creates initial content
- Evaluates it with the 20-point VEST framework
- Identifies weaknesses
- Delivers refined versions
- Shows you exactly what was improved

Perfect for high-stakes content!

### 4. Combine Modes for Nuance
```
$connect + $advise for mentoring content

$share + $story for case study insights

$update + $casual for team announcements
```

.

## 🔧 Common Use Cases

### Social Media Posts
```
Write a LinkedIn post about our 40% increase in organic traffic
```
Result: 3 versions optimized for LinkedIn engagement

### Email Campaigns
```
$advise + $casual email copy for cart abandonment
```
Result: Friendly, helpful email variations with clear CTAs

### Case Studies
```
$story about how we helped a B2B client triple their leads
```
Result: Narrative-driven case study with data points

### Team Updates
```
$update + $fun announcing our marketing team's award win
```
Result: Celebratory internal communication options

### Educational Content
```
$share + $educational how to calculate customer lifetime value
```
Result: Teaching-focused content with examples

.

## 🎯 Best Practices

### 1. Be Specific About Your Need
Instead of: `write something`
Try: `write a LinkedIn post about our new pricing strategy launch`

### 2. Include Key Details
Instead of: `case study`
Try: `case study about increasing SaaS trial conversions from 2% to 8%`

### 3. Specify Audience When Relevant
```
$advise small business owners on social media marketing with limited budget
```

### 4. Use Tone Combinations Wisely
✅ Good: `$casual + $educational`
❌ Avoid: `$fun + $formal` (conflicting tones)

### 5. Request Specific Metrics
```
Include these results: 47% CTR increase, $50K saved, 3-month timeline
```

.

## 🆘 Troubleshooting

### "It's not writing in Sarah's voice"
- Make sure you're in the Personal Branding Writer project
- Check that system instructions are properly saved
- Try using explicit mode commands: `$share [your request]`

### "I want a different voice/personality"
- Use the Prompt Improver customization method (see top of guide)
- Modify the system instructions to match your brand voice
- Keep the framework structure for consistency

### "The content seems too long"
- Use `+ $minimal` tone modifier
- Specifically request: "Keep under 50 words"
- Choose the "most concise" variation

### "I need more than 3 variations"
- Make multiple requests with different modes
- Try: `$share`, then `$connect`, then `$advise` for variety
- Use tone modifiers for additional variations

.

## 📚 Examples Gallery

### Simple Marketing Insight
**Input:** `tips for better email subject lines`
**Output:** 
- Most concise: "Questions beat statements. Numbers beat words. Curiosity beats clarity."
- Most authentic: "Our team tested 10K subject lines. Winners? Questions (↑32%), numbers (↑28%), mild confusion (↑24%). 'Professional' lost every time."
- Most valuable: "Email subject line formula: [Number] + [Benefit] + [Curiosity Gap]. Example: '3 pricing mistakes costing you 40% revenue (fix by Friday).' Test this week?"

### Campaign Story
**Input:** `$story about our influencer campaign failure`
**Output:** Full narrative using STORY framework showing the failure, what was learned, and how it led to success

### Technical Guide
**Input:** `$advise + $technical on setting up conversion tracking`
**Output:** Step-by-step technical instructions with three levels of detail

### Team Update
**Input:** `$update + $casual announcing new marketing hire`
**Output:** Warm, welcoming announcement options that highlight team collaboration

.

## 🚀 Quick Reference Card

### Daily Commands:
- `$share` = Share insights (default)
- `$connect` = Build relationships  
- `$advise` = Give guidance
- `$story` = Tell campaign stories
- `$update` = Professional announcements
- `$improve` = Auto-optimize content

### Tone Modifiers:
- `+ $casual` = Conversational
- `+ $technical` = Data-focused
- `+ $educational` = Teaching mode
- `+ $fun` = Playful energy
- `+ $formal` = Professional
- `+ $minimal` = Ultra-concise

### Power Combos:
- `$share + $casual` = Friendly insights
- `$advise + $technical` = Expert guidance
- `$connect + $educational` = Teaching moments
- `$story + $minimal` = Quick case studies

Remember: Great marketing content makes the complex feel simple. This system helps you write like you market—with clarity, empathy, and respect for your audience's time.
