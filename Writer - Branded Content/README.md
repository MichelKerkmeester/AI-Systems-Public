# Branded Content Writer - User Guide

## 🚀 What is This?

This system solves the biggest content problem: **sounding like yourself at scale**.

Instead of staring at blank pages or publishing generic content, you describe what you need and get back 3 versions that actually sound like you. The secret? A mix of writing modes for different purposes, tones for different contexts, and frameworks that structure your ideas. 

**Key Benefits:**
- Write marketing content with a consistent, professional voice
- Get 3 variations of every piece (concise/authentic/valuable)
- Access proven marketing frameworks (SVC, CASE, QPT, etc.)
- Create content that drives engagement and action
- Learn from a voice that balances data with humanity

→ Your personality + proven structures = content that's on-brand.

.

## ⚡ Ready to level up?

This starter system creates on-brand content fast.

**Build it into an enterprise-ready content engine by adding:**

- Expanded library of frameworks, examples and case studies 
- Focus modes that adapt output to strategic themes such as sustainability, innovation or customer value
- Platform-specific guidelines, including frameworks, tone, and focus combination presets
- Improved request analysis, routing and response scaling guidelines
- Curated market, industry, and competitor research optimized for LLM integration
- Repositories of product or service information, either as knowledge base item or through custom MCP integration

.

## 🎨 PRO TIP: Make This YOUR Brand Voice!

**Transform this system into your personal or company brand voice using my [Prompt Improver](https://github.com/MichelKerkmeester/AI-Systems-Public/tree/main/Writer%20-%20Prompt%20Improver)!**

This system comes configured as "Sarah Chen" - a marketing leader with specific traits and experiences. But you can instantly customize it to match YOUR unique voice, industry, and expertise.

**Example customization prompt:**
```
$full Improve this prompt '''
Transform the Branded Content Writer system into a [YOUR ROLE] writer for [YOUR BRAND].

Current system: Sarah Chen, marketing leader, 10+ years, data-driven storytelling
Target system: [YOUR NAME/BRAND], [YOUR ROLE], [YOUR EXPERIENCE], [YOUR VOICE TRAITS]

Keep the framework structure and 3-variation output system.
'''
```

See the full "Customization" section below for detailed instructions.

.

## 🎯 Full Customization Guide

### Transform Into ANY Brand Voice
The Branded Content Writer system is fully customizable. While it comes configured as "Sarah Chen" (a marketing leader), you can adapt it to any role, industry, or brand voice.

**Quick customization with [Prompt Improver](https://github.com/MichelKerkmeester/AI-Systems-Public/tree/main/Writer%20-%20Prompt%20Improver):**

```
$full Improve this prompt '''
Transform the Branded Content Writer system (currently configured as Sarah Chen, marketing leader) into a [YOUR ROLE] writer system for [YOUR COMPANY/BRAND].

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
Transform the Branded Content Writer system into a technical documentation writer system for a developer-focused SaaS company.

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
4. Name it "Branded Content Writer" (or your customized version)

### Step 2: Add the System Instructions
1. In your project, click "Edit project details"
2. Find the "Custom instructions" section
3. Copy and paste the main system file: `Writer - Branded Content - v2.04.md`
4. Save the project

### Step 3: Upload Supporting Documents
Upload these documents to your project knowledge base:
- `Artifact Standards & Templates.md` (mandatory artifact structures)
- `Copywriter Frameworks.md` (all writing frameworks)

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
The system has four specialized modes:

| Mode | Command | Use For | Example Output Style |
|------|---------|---------|---------------------|
| **Write** | `$write` or `$w` (DEFAULT) | General content needs | Balanced marketing insights |
| **Share** | `$share` or `$s` | Knowledge & insights | "Here's what worked..." |
| **Connect** | `$connect` or `$c` | Building relationships | "Ever notice how we all..." |
| **Improve** | `$improve` or `$i` | Optimize content | Full VEST evaluation + refined versions |

### Mode Examples:
```
$write a post about marketing automation best practices

$share insights from our email campaign

$connect with other marketers about budget constraints

$improve [creates content then automatically refines it]
```

.

## 🎨 Tone Modifiers

### Add Tones for Different Contexts
Combine modes with tones for precise voice control:

| Tone | Code | Best For |
|------|------|----------|
| **Natural** | `$natural` (DEFAULT) | Authentic voice with genuine uncertainty |
| **Casual** | `$casual` | Social media, team updates |
| **Technical** | `$technical` | Data reports, analytics |
| **Educational** | `$educational` | Tutorials, guides |
| **Minimal** | `$minimal` | Ad copy, headlines |

### Tone Combination Examples:
```
$write + $casual a social media post about our new feature

$share + $casual insights about influencer marketing

$write + $technical on setting up GA4 conversion tracking

$connect + $educational about marketing measurement challenges
```

.

## ✅ Output Format

### Every Response Includes:
1. **Always in an artifact** (text/markdown format)
2. **Mandatory structure with metadata:**
   - Framework used (if applicable)
   - Mode (write/share/connect/improve)
   - Tone (natural by default)
   - Platform (if specified)
   - Context (from your query)
3. **3 variations minimum:**
   - **Most concise:** Fewest words, maximum impact
   - **Most authentic:** Natural Sarah voice with stories
   - **Most valuable:** Maximum actionable takeaway

### Example Output Structure:
```
FRAMEWORK: SVC (Situation•Value•Connection)
MODE: $write
TONE: $natural
PLATFORM: LinkedIn
CONTEXT: A/B testing importance for marketers

Stock photos killed our CTR. Real employees increased it by 47%.

---

## Variations

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

### 4. Natural Voice is Default
The system defaults to `$natural` tone - authentic voice with:
- Genuine uncertainty ("Still figuring out why...")
- Conversational fragments
- Real campaign stories
- Team credit naturally included

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
$write for small business owners about social media marketing with limited budget
```

### 4. Trust the Default Mode
The system defaults to `$write` with `$natural` tone - this works for 80% of requests!

### 5. Request Specific Metrics
```
Include these results: 47% CTR increase, $50K saved, 3-month timeline
```

.

## 🆘 Troubleshooting

### "It's not writing in Sarah's voice"
- Make sure you're in the Branded Content Writer project
- Check that all 3 documents are uploaded to knowledge base
- System instructions should be in project settings

### "I want a different voice/personality"
- Use the Prompt Improver customization method (see top of guide)
- Modify the system instructions to match your brand voice
- Keep the framework structure for consistency

### "The content seems too long"
- Use `+ $minimal` tone modifier
- Specifically request: "Keep under 50 words"
- Choose the "most concise" variation

### "I need more than 3 variations"
- Ask explicitly: "Create 5 variations"
- Try different mode combinations
- Use tone modifiers for additional variations

### "Framework selection seems off"
- Specify framework directly: "Use SVC framework"
- Or request: "Write naturally without framework"
- Remember: Simple edits don't need frameworks!