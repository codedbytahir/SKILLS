name: design-taste-development
description: >
Develop and refine design taste as a developer. Analyze what makes UI look premium vs amateur,
evaluate color choices, typography, spacing, and visual hierarchy. Use when the user asks to
"make it look better", "improve the design", "does this look good", or needs design feedback
on a component, page, or entire interface.
Design Taste Development for Developers
Overview
Design taste is the ability to distinguish between good and bad visual design, and more importantly,
to understand why something looks good or bad. It is not about being artistic — it is about
developing a trained eye for visual quality, consistency, and intentionality in UI design.

Source & Credit: Synthesized from "Developing Design Taste as a Developer" and the broader
teaching of Manu Arora (@mannupaaji on X, youtube.com/@manuarora), creator of Aceternity UI.

When to Use This Skill
User asks "make it look better" or "improve the design"
User asks for design feedback or review
Building UI components that need a polished, premium feel
Evaluating or recreating designs from high-quality reference sites
Any task where visual quality of the output matters
Core Principles
1. The Taste Gap
Taste develops faster than ability. You will recognize bad design before you can consistently
produce good design. This is normal and expected. The gap between your taste and your ability
is what drives improvement. Never lower your standards — raise your skills to meet them.

2. Build a Reference Library
Curate a personal collection of designs you admire. When you see a website, app, or component
that looks exceptional, save it. Organize by category: landing pages, dashboards, cards,
animations, color palettes, typography combinations. You cannot build what you cannot imagine.

Practical action: Maintain a bookmark folder or Notion board called "Design References"
with at least 50 entries across different categories.

3. Deconstruct, Don't Just Admire
When you see a beautiful design, do not just appreciate it — break it down:

Spacing: What is the padding/margin rhythm? Is it 4px, 8px, 16px, 24px, 32px, 48px, 64px?
Premium designs almost always use a consistent spacing scale (typically powers of 2).
Typography: How many font sizes are used? What is the ratio between heading and body?
Is there a clear type scale (e.g., 14/16/20/24/32/40/48)?
Color palette: How many colors are actually used? Premium designs rarely use more than
3-4 colors. Identify the primary, secondary, accent, and neutral colors.
Borders and shadows: Are borders used? How heavy are shadows? Premium designs use
subtle shadows (very low blur, very low opacity) or no shadows at all.
Border radius: Is it consistent? Premium designs use consistent border radius values
(e.g., 8px, 12px, 16px, or full rounded for pills/badges).
4. Spacing Is the Single Biggest Differentiator
Most amateur designs fail on spacing, not color or typography. The difference between a
premium and amateur UI is often just consistent, generous spacing.

Rules:

Use a spacing scale: 4, 8, 12, 16, 20, 24, 32, 40, 48, 64, 80, 96
Elements should breathe — when in doubt, add more padding
Group related items closer, separate unrelated items further (Gestalt proximity principle)
Vertical rhythm matters: maintain consistent spacing between sections
Never use arbitrary values like padding: 13px or margin: 37px
5. Color Discipline
Amateur designers use too many colors. Professional designers are extremely disciplined:

Start with one color (the brand/accent color)
Add a neutral palette (grays for text, backgrounds, borders)
Use opacity variations of your accent color instead of adding new colors
Dark backgrounds need lighter text with lower contrast than you think (pure white #FFF
on dark backgrounds is harsh — try rgba(255,255,255,0.9) or rgba(255,255,255,0.8))
Gradients should be subtle. Avoid rainbow gradients. Two-color gradients with similar
hues (e.g., from purple to blue) look more premium than complementary color gradients.
6. Typography Hierarchy
Good typography creates a clear reading order:

Use 2-3 font sizes maximum for body content areas
Headings should be dramatically larger than body text (1.5x-2.5x ratio)
Line height for body text: 1.5-1.7 (never less than 1.4)
Line height for headings: 1.1-1.3 (tighter than body)
Letter spacing: body text at default or -0.01em, headings at -0.02em to -0.04em
Font weight: use 400 for body, 500-600 for emphasis, 700+ only for main headings
Limit to 1-2 font families maximum
7. Simplicity and Restraint
The most common mistake is adding too much. Premium designs are characterized by what they
remove, not what they add.

If a visual element does not serve a purpose, remove it
Avoid decorative elements that don't add information or guide attention
White space (negative space) is not empty space — it is a design element
A clean, minimal design always beats a cluttered one
When you finish a design, go back and remove 20% of what you added
8. The "Does It Look Like a Real Product?" Test
Before shipping any UI, ask:

Would I be proud to show this to a senior designer?
Does this look like it could belong on a product from Apple, Linear, Vercel, or Stripe?
Are there any visual inconsistencies (different border radius, different shadow styles,
inconsistent spacing)?
Would a user trust this interface with their money/data?
Evaluation Checklist
When reviewing or building UI, score each category 1-5:

Category
Question
Spacing	Is spacing consistent and follows a scale?
Color	Are colors limited (3-4 max) and harmonious?
Typography	Is there a clear hierarchy with 2-3 sizes?
Consistency	Are border-radius, shadows, and styles uniform?
Whitespace	Does the design breathe? Is nothing cramped?
Contrast	Is text readable? Is the visual hierarchy clear?
Alignment	Are elements aligned to a grid?
Restraint	Is anything unnecessary or decorative?

Score 30+ = Premium quality. Score 20-29 = Good, needs polish. Score below 20 = Needs fundamental redesign.

Anti-Patterns to Avoid
Using more than 4 colors in a single view
Inconsistent border-radius values (mixing 4px, 8px, 12px randomly)
Heavy drop shadows (shadow blur > 20px, opacity > 0.15)
Too many font sizes or font families
Cramped layouts with insufficient padding
Using pure black (#000) text on light backgrounds (use #111 or #1a1a1a instead)
Using pure white (#FFF) text on dark backgrounds (use rgba(255,255,255,0.9))
Gradient backgrounds that are too saturated
Borders that are too dark or too thick (use very subtle borders: 1px with low-opacity colors)
Centered text for everything (use left-aligned for readability)
Mixing rounded and sharp corners without intention
