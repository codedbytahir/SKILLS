name: color-typography-systems
description: >
Build cohesive color and typography systems for web products. Covers color palette
construction, dark mode implementation, type scales, font pairing, and the visual
hierarchy principles that make text readable and designs harmonious. Use when setting
up a design system, choosing colors, selecting fonts, implementing dark mode, or when
the user asks about color/typography choices.
Color and Typography Systems
Overview
Color and typography are the two most impactful visual design decisions you will make.
Getting them right creates an immediate impression of quality. Getting them wrong makes
even the best layout look amateurish. This skill provides a systematic approach to
building color palettes and typography systems that work together harmoniously.

Source & Credit: Synthesized from the design principles taught across Manu Arora's
content (youtube.com/@manuarora), particularly from "Developing Design Taste as a Developer",
the visual philosophy of Aceternity UI (ui.aceternity.com), and observations from the
"Steal This Design" series analyzing Apple, Dia Browser, and other premium products.

When to Use This Skill
Setting up a new project's color palette or typography
Implementing dark mode
Choosing fonts for a web project
Fixing readability or visual hierarchy issues
Building a design system or component library
User asks "what colors should I use" or "what fonts go well together"
Building a Color System
Step 1: Start with the Accent Color
Choose ONE accent color. This is the color that will represent your brand/product.

Selection criteria:

Should be distinctive and memorable
Should work well at small sizes (icons, badges) and large sizes (heroes, backgrounds)
Should have enough saturation to stand out but not so much that it feels garish
Test it on both light and dark backgrounds
Step 2: Build the Neutral Palette
The neutral palette does 80% of the work. Build it carefully:

text

Light Mode:
  Background:    #FAFAFA or #F5F5F7 (warm off-white, never pure white for large areas)
  Surface:       #FFFFFF (cards, modals — pure white is fine for elevated elements)
  Border:        rgba(0, 0, 0, 0.06) (barely visible, just enough to separate)
  Text Primary:  #111111 or #1A1A1A (near-black, never pure black)
  Text Secondary: #6B7280 (medium gray, for descriptions and meta text)
  Text Tertiary: #9CA3AF (light gray, for placeholders and hints)

Dark Mode:
  Background:    #0A0A0A (rich dark, never pure black)
  Surface:       #141414 or #1A1A1A (elevated elements)
  Border:        rgba(255, 255, 255, 0.06)
  Text Primary:  rgba(255, 255, 255, 0.9) (not pure white)
  Text Secondary: rgba(255, 255, 255, 0.6)
  Text Tertiary: rgba(255, 255, 255, 0.4)
Step 3: Generate Opacity Variants of Accent
Instead of adding more colors, use opacity variations:

css

.accent-foreground { color: your-accent-color; }
.accent-muted      { color: your-accent-color / 0.7; }
.accent-subtle     { color: your-accent-color / 0.5; }
.accent-faint      { color: your-accent-color / 0.3; }
This creates a cohesive palette without introducing disharmonious new hues.

Step 4: Add ONE Optional Secondary Accent
If you need a second color (for success/error/warning states, or a complementary accent):

Choose from the same hue family (analogous) for harmony
Or choose from the opposite side of the color wheel (complementary) for contrast
Never add more than 2 accent colors
Step 5: Define Semantic Colors
css

--success: #22C55E;  /* or a muted green like #4ADE80 */
--warning: #F59E0B;  /* or #FBBF24 */
--error:   #EF4444;  /* or #F87171 */
--info:    #3B82F6;  /* or #60A5FA */
Keep semantic colors muted. Bright red error states feel aggressive.

Dark Mode Implementation Strategy
Approach: CSS Variables with class toggle

css

:root {
  --background: #FAFAFA;
  --foreground: #111111;
  --muted: #F5F5F5;
  --muted-foreground: #6B7280;
  --border: rgba(0, 0, 0, 0.06);
  --accent: #6366F1;
  --accent-foreground: #FFFFFF;
  --card: #FFFFFF;
  --card-foreground: #111111;
}

.dark {
  --background: #0A0A0A;
  --foreground: rgba(255, 255, 255, 0.9);
  --muted: #1A1A1A;
  --muted-foreground: rgba(255, 255, 255, 0.6);
  --border: rgba(255, 255, 255, 0.06);
  --accent: #818CF8;  /* slightly lighter for dark mode */
  --accent-foreground: #0A0A0A;
  --card: #141414;
  --card-foreground: rgba(255, 255, 255, 0.9);
}
Key dark mode rules:

Never use pure black (#000000) — it creates too much contrast
Never use pure white text on dark backgrounds — use rgba(255,255,255,0.9)
Borders should be even more subtle in dark mode
Accent colors may need to be lightened 10-20% for visibility
Shadows in dark mode should use the accent color at very low opacity, not black
Building a Typography System
Font Selection
For body text (UI font):

Font
Character
Best For
Inter	Clean, neutral, highly readable	General purpose, dashboards, SaaS
Geist	Sharp, modern, slightly condensed	Developer tools, tech products
Plus Jakarta Sans	Friendly, rounded terminals	Consumer products, startups
Manrope	Geometric, clean	Modern web apps
DM Sans	Humanist, warm	Content-heavy sites

For headings (display font):

Font
Character
Best For
Same as body (heavier weight)	Consistent, clean	Most products
Cal Sans	Geometric, distinctive	Developer tools
Newsreader	Serif, editorial	Content sites, blogs
Playfair Display	Elegant serif	Luxury, editorial

Rule: For most products, use ONE font family. Use weight and size to create hierarchy.
Two fonts is the maximum (one for body, optionally one for display headings).

Type Scale
Use a consistent type scale. This is the recommended scale for modern web products:

text

xs:       12px / weight 500 / line-height 1.5  — labels, captions, badges
sm:       14px / weight 400 / line-height 1.5  — secondary text, meta
base:     16px / weight 400 / line-height 1.6  — body text, paragraphs
lg:       18px / weight 400 / line-height 1.6  — large body text
xl:       20px / weight 500 / line-height 1.4  — section subheadings
2xl:      24px / weight 600 / line-height 1.3  — card titles, small headings
3xl:      30px / weight 600 / line-height 1.2  — section headings
4xl:      36px / weight 700 / line-height 1.15 — page headings
5xl:      48px / weight 700 / line-height 1.1  — hero headings
6xl:      60px / weight 700 / line-height 1.05 — display text
7xl:      72px / weight 700 / line-height 1    — large display
Letter Spacing Guidelines
text

Display/Headings:  -0.03em to -0.04em (tighter, looks premium)
Body text:          0 or -0.01em (default)
ALL CAPS/Labels:    +0.05em to +0.1em (needs more space)
Monospace:          0 (never adjust)
Line Height Guidelines
text

Headings (3xl+):    1.05 - 1.2  (tight, compact)
Subheadings (xl-2xl): 1.3 - 1.4
Body text (base-lg):  1.5 - 1.7  (comfortable reading)
Small text (xs-sm):   1.5        (never less than body)
Text Color Hierarchy
A page should have at most 3 levels of text emphasis:

text

Level 1 (Primary):   foreground color, regular or semibold weight
Level 2 (Secondary): muted-foreground color, regular weight
Level 3 (Tertiary):  even more muted, smaller size or lighter weight
If everything is the same color and size, nothing stands out. If everything is bold,
nothing is bold. Hierarchy requires contrast.

Quick Reference: Tailwind CSS Implementation
js

// tailwind.config.js
module.exports = {
  theme: {
    extend: {
      colors: {
        border: "hsl(var(--border))",
        background: "hsl(var(--background))",
        foreground: "hsl(var(--foreground))",
        primary: {
          DEFAULT: "hsl(var(--primary))",
          foreground: "hsl(var(--primary-foreground))",
        },
        muted: {
          DEFAULT: "hsl(var(--muted))",
          foreground: "hsl(var(--muted-foreground))",
        },
        accent: {
          DEFAULT: "hsl(var(--accent))",
          foreground: "hsl(var(--accent-foreground))",
        },
      },
      fontFamily: {
        sans: ["var(--font-sans)", "system-ui", "sans-serif"],
      },
    },
  },
};
Anti-Patterns
Using more than 2 font families
Using more than 5 distinct font sizes in a single view
Pure black text on pure white background (harsh on the eyes)
Low-contrast text (gray text on light gray background)
Inconsistent text colors (mixing hardcoded colors and CSS variables)
Using font-weight: 900 or bold for body text
Center-aligned paragraphs (hard to read, always left-align body text)
Line height below 1.4 for body text
All-caps for more than a few words (labels and badges only)
Decorative fonts for body text
