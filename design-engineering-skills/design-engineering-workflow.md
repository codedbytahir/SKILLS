name: design-engineering-workflow
description: >
The end-to-end workflow of a design engineer: from concept to production-ready UI.
Covers the intersection of design thinking and frontend engineering, including design
tools, code-design handoff, component architecture, and the mindset of building
beautiful products. Use when the user wants to start with design engineering,
needs a workflow for building UI from scratch, or asks about the design engineer role.
Design Engineering Workflow
Overview
Design engineering is the discipline of building UI at the intersection of design and code.
A design engineer thinks like a designer but ships like an engineer. They do not just
implement pixel-perfect designs — they make design decisions, understand visual principles,
and translate aesthetic intent into production code. This skill covers the complete workflow
from concept to shipped product.

Source & Credit: Synthesized from "How to Get Started with Design Engineering in 2025",
"The Only Tools I Actually Use as a Design Engineer", "Frontend Developer vs Design Engineer
vs UI Developer", and the broader body of work by Manu Arora
(youtube.com/@manuarora, manuarora.in), creator of Aceternity UI and design engineer at
Aceternity studio.

When to Use This Skill
User wants to understand or practice design engineering
Building a product UI from scratch (no designer, no design file)
Setting up a design engineering workflow or toolchain
Deciding between design tools and approaches
Building a component library or design system
The Design Engineer Mindset
Frontend Developer vs Design Engineer vs UI Developer
Role
Primary Focus
Key Skill
Frontend Developer	Logic, state, data flow, performance	React, state management, APIs
UI Developer	Implementing designs from Figma/Sketch files accurately	CSS, responsive, accessibility
Design Engineer	Making design decisions AND implementing them	Visual taste + frontend skills + design thinking

A design engineer can do all three. They do not need a Figma file to build something
beautiful — they have the taste and principles to make design decisions in code.

Core Principles
Ship, don't just design. Every design decision should be evaluated against
implementation cost. A design that cannot be built is a worthless design.
Iterate in code, not in design tools. The fastest way to evaluate a visual
decision is to see it rendered in the browser. Design tools are for exploration;
the browser is for validation.
Build components, not pages. Think in reusable, composable pieces. Every piece
of UI you build should be a candidate for your component library.
Taste is a skill, not a talent. It can be developed through study, practice,
and deliberate exposure to great design.
The Workflow
Phase 1: Research and Reference Gathering
Before writing any code:

Identify 3-5 reference designs — Find products or websites whose aesthetic
matches what you are going for. Screenshot them.
Extract the design system — From each reference, identify: colors, typography,
spacing, border-radius, shadow style, animation style.
Create a mood board — Combine the best elements from each reference into a
cohesive visual direction.
Define the component inventory — List every component you will need: buttons,
cards, inputs, modals, navigation, etc.
Phase 2: Foundation Setup
Before building any components:

Choose your tech stack: Next.js + Tailwind CSS + Framer Motion is the recommended
stack for design engineering (this is what Manu Arora uses for Aceternity UI).
Set up your design tokens:
css

/* tailwind.config.js */
module.exports = {
  theme: {
    extend: {
      colors: {
        background: "var(--background)",
        foreground: "var(--foreground)",
        muted: { DEFAULT: "var(--muted)", foreground: "var(--muted-foreground)" },
        border: "var(--border)",
      },
      fontFamily: {
        sans: ["var(--font-sans)"],
        mono: ["var(--font-mono)"],
      },
      borderRadius: {
        lg: "var(--radius)",
        md: "calc(var(--radius) - 2px)",
        sm: "calc(var(--radius) - 4px)",
      },
    },
  },
};
Define your spacing scale and stick to it: 4, 8, 12, 16, 20, 24, 32, 40, 48, 64, 80, 96
Set up a type scale: 12, 14, 16, 18, 20, 24, 30, 36, 48, 60, 72
Phase 3: Component Architecture
Build components in this order (bottom-up):

Primitives: Button, Input, Badge, Avatar, Separator
Composites: Card, Dialog, Dropdown, Tooltip, Tabs
Patterns: Hero section, Feature grid, Testimonial, Pricing table, Footer
Templates: Landing page, Dashboard, Blog, Documentation
Component design rules:

Every component should work independently (no hidden parent dependencies)
Use composition over configuration (slot pattern, not 50 props)
Animations should be built-in but toggleable via a prop
Support both light and dark mode from the start
Phase 4: Build and Iterate
Build the hero section first — It sets the visual tone for the entire product
Use browser DevTools extensively — The inspect tool is your best design tool
Iterate rapidly — Make a change, see it in the browser, adjust. Repeat.
Test on real content — Placeholder text reveals nothing. Use real copy ASAP.
Test at all breakpoints — Design that works on desktop but breaks on mobile
is not done.
Phase 5: Polish and Ship
Animation pass: Add entry animations, hover states, transitions
Accessibility pass: Check color contrast, keyboard navigation, screen readers
Performance pass: Audit for layout shifts, unnecessary re-renders, image optimization
Cross-browser test: Chrome, Firefox, Safari (especially Safari for animations)
Ship and gather feedback — Real user feedback > your own opinion
Design Engineer Tool Stack
Based on Manu Arora's recommended toolkit:

Design Exploration
Figma — For quick exploration, mood boarding, and sharing ideas with collaborators
Real product websites — The best design inspiration comes from shipping products
Development
VS Code / Cursor — Code editor (Cursor adds AI assistance)
Next.js — Framework (App Router for new projects)
Tailwind CSS — Utility-first styling (v4 preferred)
Framer Motion — Animation library for React
Inspiration & References
Aceternity UI (ui.aceternity.com) — 200+ copy-paste components
Dribbble / Awwwards — For discovering new design trends
Tailwind UI / shadcn/ui — For base component patterns
Real SaaS products — Stripe, Linear, Vercel, Raycast for reference
Asset Creation
Favicon.io — Quick favicon generation
Spline — 3D elements for web
Unsplash / Pexels — High-quality free photography
Component Library Philosophy
If you are building a component library (like Aceternity UI):

Every component must be copy-pasteable — No complex setup, no required context
Tailwind classes inline — No separate CSS files, no CSS modules
Framer Motion for animations — Consistent animation API
TypeScript — Full type safety for props
Minimal dependencies — React, Next.js, Tailwind, Framer Motion. That is it.
Preview-driven development — Build the preview first, see it rendered, then abstract
Income Streams for Design Engineers
From Manu Arora's "5 Income Hacks Every Design Engineer Should Know":

Aceternity UI model: Build a free component library, monetize with a Pro tier
Consulting: Charge $100-300/hr for design engineering consultation
YouTube/Twitter: Build an audience teaching design engineering
Sponsorships: Brand deals on content (tools, hosting, SaaS products)
Client work: Build premium websites for startups and enterprises
Anti-Patterns
Spending weeks in Figma before writing any code
Building a design system without first building real products
Choosing tools based on trends rather than project needs
Ignoring mobile/responsive design until the end
Over-engineering component abstractions before understanding usage patterns
