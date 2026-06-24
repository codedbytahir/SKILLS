name: steal-this-design-analysis
description: >
Analyze and recreate premium UI designs from real-world products. Break down what makes
a design look premium by deconstructing spacing, color, typography, layout, and interaction
patterns. Use when the user wants to "recreate X design", "make it look like Y website",
"analyze this UI", or build interfaces inspired by specific premium products.
Steal This Design: Premium UI Analysis & Recreation
Overview
"Steal This Design" is the practice of analyzing exceptional UI designs from real products,
understanding what makes them work, and applying those principles to your own work. This is
not about copying — it is about developing your design eye by studying the best work in the
industry and understanding the specific techniques that create a premium feel.

Source & Credit: Based on the "Steal This Design" series by Manu Arora
(youtube.com/@manuarora), where he breaks down and recreates designs from Apple, Dia Browser,
and other premium products. Additional insights from The Browser Company's design strategy
for Dia Browser (browsercompany.substack.com).

When to Use This Skill
User wants to recreate or draw inspiration from a specific product's design
User asks "why does X website look so good?"
Building a landing page or product page that needs a premium feel
Analyzing competitor designs or design references
Teaching or learning design principles through real examples
The Analysis Framework
When you encounter a design worth studying, systematically analyze it across these dimensions:

1. Layout Architecture
What to look for:

What is the overall grid structure? (centered single column, two-column, full-width sections)
What is the max content width? Premium sites typically use 1200-1400px max-width
How is whitespace used between sections? (typically 80-160px vertical padding)
Is the layout symmetric or asymmetric? Premium designs often use subtle asymmetry
How does the layout adapt on mobile?
Key insight from Manu Arora's Dia Browser analysis: Premium designs use generous
section spacing (100-150px between major sections) and maintain a clear visual rhythm.
Each section has a distinct purpose and breathing room.

2. Color System Deconstruction
Extract the exact color palette:

Role
Typical Pattern
Background	Very subtle gradient or solid near-white (#FAFAFA, #F5F5F7, or pure #FFF)
Primary text	Near-black, never pure black (#0A0A0A, #111111, #1D1D1F)
Secondary text	Medium gray (#6B7280, #86868B, #A1A1AA)
Accent	One bold color used sparingly (for CTAs, links, highlights)
Borders	Very subtle (rgba(0,0,0,0.05) to rgba(0,0,0,0.1))

Dark mode patterns:

Background: #0A0A0A to #111111 (never pure black)
Text: rgba(255,255,255,0.9) for primary, rgba(255,255,255,0.6) for secondary
Borders: rgba(255,255,255,0.05) to rgba(255,255,255,0.1)
Accent: Slightly desaturated or higher-brightness version of the light mode accent
3. Typography System
Extract the type scale:

text

Display:    48-72px / weight 600-700 / letter-spacing -0.03em
H1:         36-48px / weight 600 / letter-spacing -0.025em
H2:         28-36px / weight 600 / letter-spacing -0.02em
H3:         20-24px / weight 500 / letter-spacing -0.01em
Body:       16-18px / weight 400 / letter-spacing 0
Small:      14px / weight 400 / letter-spacing 0
Caption:    12px / weight 500 / letter-spacing 0.05em (uppercase for labels)
Font choices observed in premium designs:

Inter — the workhorse. Clean, readable, modern. Used by Vercel, Linear.
Geist — Vercel's custom font, similar to Inter but sharper.
SF Pro — Apple's system font. Premium by association.
Plus Jakarta Sans — Used by many modern SaaS products.
4. Spacing and Rhythm
Extract the spacing scale:

text

Component padding:    16-24px
Card padding:         24-32px
Section padding:      64-96px (vertical)
Section gap:          80-120px (between sections)
Container max-width:  1200-1400px
Container padding:    16-24px (mobile), 24-48px (desktop)
5. Component Patterns
Cards:

Border: 1px solid rgba(0,0,0,0.05) or no border with subtle shadow
Border radius: 12-16px
Shadow: 0 1px 3px rgba(0,0,0,0.05) — extremely subtle
Hover: Slight scale (1.01-1.02) or shadow increase
Padding: 24-32px
Buttons:

Primary: Solid background, white text, border-radius 8-12px, padding 10-14px 20-28px
Secondary: Transparent background, 1px border, same text as primary
Font weight: 500, font size: 14-16px
Hover: Subtle brightness shift or background color change
Navigation:

Fixed or sticky, with backdrop blur
Logo left, links center or right
CTA button on the right
Height: 64-72px
Border bottom: 1px solid rgba(0,0,0,0.05)
6. Interaction and Animation Patterns
Premium designs use animation purposefully, not decoratively:

Page load: Elements fade in with slight upward translation (translateY: 20px → 0)
Hover states: Subtle scale (1.01-1.02), shadow transition, or color shift
Scroll reveals: Staggered fade-in as sections enter the viewport
Page transitions: Cross-fade or slide transitions between pages
Micro-interactions: Button press effect (scale 0.98), toggle switches, accordion expands
Timing guidelines:

Hover: 150-200ms
Page transitions: 300-500ms
Scroll reveals: 500-800ms
Stagger delay: 50-100ms between sibling elements
Recreation Process
When tasked with recreating a design:

Screenshot the reference at full resolution
Extract colors using a color picker from the screenshot
Identify the grid — draw lines to find alignment points
Count font sizes — measure heading and body text sizes
Measure spacing — use a pixel ruler or browser dev tools
Identify the font — use WhatTheFont or similar tools
List all components — header, hero, features, testimonials, CTA, footer
Build section by section — start with layout, then color, then typography, then animations
Compare side-by-side — put your version next to the original
Iterate on differences — the first version will not match. Close the gap.
Case Study: Dia Browser Design
From Manu Arora's "Steal This Design" analysis of Dia Browser:

What makes it feel premium:

Restraint: Very few colors, lots of whitespace, no decorative elements
Typography hierarchy: One font (system), dramatic size differences between headings and body
Subtle depth: No heavy shadows, using only very faint borders and background color differences
Generous spacing: Each section has room to breathe
No duplicative UI: Every element serves a unique purpose — nothing is repeated unnecessarily
Dark mode first: The dark theme uses true dark colors (#0A0A0A) with carefully adjusted text opacity
Visual interest through simplicity: The interest comes from what is NOT there
Anti-Patterns
Do not pixel-perfect copy a design (legal issues, and it shows lack of taste)
Do not recreate the layout without understanding WHY those choices were made
Do not add your own decorative elements that break the original's restraint
Do not use the exact same copy/text as the original
Do not ignore responsiveness — the original likely works on all screen sizes
