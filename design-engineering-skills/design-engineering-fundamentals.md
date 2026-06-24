name: design-engineering-fundamentals
description: >
The foundational principles every design engineer must know: visual hierarchy,
Gestalt principles, spacing systems, border-radius strategy, shadow philosophy,
responsive design patterns, and the difference between "looks fine" and "looks
premium". Use as a reference when making any visual design decision, when the
user asks "why doesn't this look good", or as a design review checklist.
Design Engineering Fundamentals
Overview
These are the non-negotiable foundational principles that separate professional UI from
amateur work. They are not trends — they are timeless design fundamentals that apply
to every web interface regardless of framework, style, or audience. Internalize these
and every UI you build will be better.

Source & Credit: Core principles synthesized from the complete body of work by
Manu Arora (youtube.com/@manuarora, manuarora.in, ui.aceternity.com), combining
insights from "Developing Design Taste as a Developer", the "Steal This Design" series,
Aceternity UI component patterns, and his design engineering workflow content.

When to Use This Skill
As a reference when making ANY visual design decision
When the user asks "why doesn't this look right?"
During design reviews or feedback sessions
As a checklist before shipping any UI
When teaching or learning design fundamentals
1. Visual Hierarchy
Visual hierarchy is the arrangement of elements in order of importance. Without it,
users do not know where to look.

How to Create Hierarchy
Size (most powerful):

The most important element should be the largest
A 48px heading commands more attention than a 16px paragraph
Use a ratio of at least 1.5x between heading levels
Color/Contrast:

High contrast = high importance (bold accent color on CTA button)
Low contrast = low importance (muted text for timestamps, metadata)
Never make everything high contrast — the result is visual noise
Whitespace:

More whitespace around an element = more importance
Isolate your most important element with generous spacing
Crowded elements feel equally (un)important
Position:

Top-left is where Western readers look first (F-pattern)
Center works for hero content and key messages
Right side is good for actions/CTAs (natural flow end)
Weight:

Bold/heavy elements attract attention
Use font-weight sparingly — bold everything = bold nothing
Hierarchy Test
Squint at your design (or apply a 10px Gaussian blur). Can you still identify:

The most important element? (Should stand out clearly)
The second most important element?
The action you want the user to take?
If not, your hierarchy is broken.

2. Gestalt Principles in UI
The human brain automatically groups visual elements. Use these principles intentionally:

Proximity
Elements close together are perceived as related. Use this for:

Grouping form labels with their inputs
Grouping metadata (date, author, category) together
Separating unrelated content with more whitespace
Similarity
Elements that look similar are perceived as related. Use this for:

Consistent button styles across the page
Consistent card layouts in a grid
Consistent typography within the same content type
Continuity
The eye follows smooth paths. Use this for:

Alignment along a single axis (left-aligned text, grid columns)
Visual flow from one section to the next
Guiding the eye from heading → description → CTA
Closure
The brain fills in missing information. Use this for:

Borders with very low opacity (the brain completes the box)
Partially visible elements hinting at more content
Card hover effects that reveal more
Figure-Ground
Elements must be clearly distinguishable from their background. Use this for:

Sufficient contrast between text and background
Cards elevated with subtle shadow or border from the page background
Modal overlays darkening the background
3. The Spacing System
Spacing is the invisible architecture of good design.

The 4-Base Scale
All spacing should be derived from a base unit (4px) and its multiples:

text

4px   — micro spacing (icon padding, badge padding, inline gaps)
8px   — tight spacing (between related inline elements, small gaps)
12px  — compact spacing (form element padding, list item gaps)
16px  — standard spacing (default padding, paragraph margins)
20px  — comfortable spacing (card padding on mobile)
24px  — generous spacing (card padding on desktop, section sub-gaps)
32px  — section spacing (between related sections)
40px  — large section spacing
48px  — major section spacing (between content blocks)
64px  — page section spacing (between major page sections)
80px  — hero section padding
96px  — large section padding
128px — maximum section padding (for landing page sections)
Rules
Never use arbitrary values. If you find yourself writing padding: 13px or
margin: 37px, you have made a spacing error.
Double the gap between groups. If items within a group are 8px apart, groups
should be 16px apart, and sections containing groups should be 32px apart.
Consistent internal padding. All cards should have the same padding. All sections
should have the same vertical padding.
Mobile spacing is smaller. Reduce spacing by 25-50% on mobile. Do not just
scale everything — reduce the gaps.
Whitespace is a design element. It is not "empty space" — it is active negative
space that creates breathing room and emphasis.
4. Border Radius Strategy
Consistent border radius is a hallmark of professional design:

text

0px    — sharp corners (dividers, full-width sections, code blocks)
4px    — small elements (tags, small badges, inline code)
6px    — small interactive elements (small buttons, inputs)
8px    — standard buttons, inputs, dropdowns
12px   — cards, modals, large buttons
16px   — large cards, feature sections, image containers
24px   — hero sections, large containers
9999px — pills, avatars, icon buttons, circular elements
Rules:

Pick 2-3 radius values and use them consistently throughout the project
Never mix sharp and rounded corners on the same element type
Inner elements should have a smaller radius than their container
rounded-xl (12px) is the most versatile choice for cards
5. Shadow Philosophy
Shadows create depth and elevation. Most designers use shadows that are too heavy.

Shadow Scale
text

Level 0 (flat):     none
Level 1 (subtle):   0 1px 2px rgba(0,0,0,0.05)
Level 2 (low):      0 1px 3px rgba(0,0,0,0.07), 0 1px 2px rgba(0,0,0,0.05)
Level 3 (medium):   0 4px 6px rgba(0,0,0,0.07), 0 2px 4px rgba(0,0,0,0.05)
Level 4 (high):     0 10px 15px rgba(0,0,0,0.08), 0 4px 6px rgba(0,0,0,0.04)
Level 5 (modal):    0 20px 25px rgba(0,0,0,0.1), 0 8px 10px rgba(0,0,0,0.04)
Rules
Default to no shadow. Use borders instead of shadows for most elements.
When you do use shadows, use the lowest level that communicates elevation.
Shadows should have very low opacity (5-8% max for regular elements).
Never use box-shadow: 0 0 Xpx (blurred but no offset) — it looks blurry, not elevated.
In dark mode, use the accent color at very low opacity instead of black shadows.
For glass/transparent elements, use a 1px border instead of a shadow.
6. The "Premium" Checklist
Before shipping any UI, verify:

Layout
 Content is centered within a max-width container
 Grid columns are consistent within each section
 Elements are aligned to a grid (not floating randomly)
Spacing
 All spacing values follow the 4px scale
 Section padding is consistent (all sections use the same py value)
 Internal padding is consistent (all cards use the same p value)
 Nothing feels cramped — increase padding if in doubt
Color
 No more than 4 colors in any single view
 Text has sufficient contrast (WCAG AA minimum)
 Background is not pure white (#FAFAFA or #F5F5F7 for light, #0A0A0A for dark)
 Borders are very subtle (opacity 5-10%)
Typography
 Clear hierarchy: 2-3 distinct sizes per section
 Line height: 1.5-1.7 for body, 1.1-1.3 for headings
 Body text is left-aligned (never center-aligned paragraphs)
 No more than 2 font families
Interactivity
 All interactive elements have hover states
 All interactive elements have focus states (for keyboard users)
 Buttons have active/press states
 Transitions are smooth (150-300ms)
Responsiveness
 Works on mobile (320px+)
 Works on tablet (768px+)
 Works on desktop (1280px+)
 No horizontal scroll at any breakpoint
 Touch targets are at least 44x44px on mobile
> Credits
> All principles in this skill are synthesized from the teaching and work of Manu Arora:

YouTube: youtube.com/@manuarora
Website: manuarora.in
Aceternity UI: ui.aceternity.com
Twitter/X: @mannupaaji
Additional references:

CSS-Tricks SVG Line Animation: css-tricks.com/svg-line-animation-works
The Browser Company's Dia Design Strategy: browsercompany.substack.com
Agent Skills Specification: agentskills.io/specification
