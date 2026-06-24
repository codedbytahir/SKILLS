name: premium-landing-page
description: >
Build premium landing pages with hero sections, feature grids, testimonials,
pricing tables, CTAs, and footers that look and feel like they belong in a
Y Combinator-backed startup. Covers layout patterns, section composition,
scroll effects, and the visual hierarchy that converts visitors. Use when
building a landing page, product page, marketing site, or any page that
needs to look professional and convert.
Premium Landing Page Construction
Overview
A landing page is a design engineer's most common deliverable. It needs to communicate
value, build trust, and drive action — all while looking effortlessly premium. This skill
covers the section-by-section construction of a modern landing page, drawing from the
design patterns observed across Manu Arora's analyses of premium products and the
components built in Aceternity UI.

Source & Credit: Synthesized from Manu Arora's "Steal This Design" series
(Apple, Dia Browser breakdowns), "How to Get Started with Design Engineering",
component tutorials, and the landing page patterns in Aceternity UI
(ui.aceternity.com, youtube.com/@manuarora).

When to Use This Skill
Building a landing page or marketing site
Creating a product page that needs to convert
Designing hero sections, feature sections, or CTAs
User wants a "startup-quality" or "premium" website
Redesigning an existing page to look more professional
The Landing Page Architecture
A premium landing page follows this section order, though not all sections are required:

text

1. Navigation (sticky/fixed)
2. Hero Section (above the fold)
3. Social Proof Bar (logos or metrics)
4. Feature Overview (3-4 key features)
5. Feature Deep-Dive (alternating layout)
6. Testimonials / Case Studies
7. Pricing (if applicable)
8. FAQ
9. Final CTA
10. Footer
Section-by-Section Guide
1. Navigation
The nav is your first impression of design quality:

tsx

<nav className="fixed top-0 w-full z-50 border-b border-white/5 bg-background/80 backdrop-blur-xl">
  <div className="mx-auto flex h-16 max-w-6xl items-center justify-between px-6">
    <Logo />
    <div className="hidden md:flex items-center gap-8">
      <NavLinks />
    </div>
    <div className="flex items-center gap-4">
      <Button variant="ghost" size="sm">Log in</Button>
      <Button size="sm">Get Started</Button>
    </div>
  </div>
</nav>
Rules:

Height: 64px (h-16) to 72px (h-18)
Backdrop blur on scroll (backdrop-blur-xl bg-background/80)
Max content width: 1200px (max-w-6xl or max-w-7xl)
Logo left, nav links center (or right), CTA button right
Border bottom: 1px, very subtle (border-white/5 in dark, border-black/5 in light)
Mobile: hamburger menu or simple icon row
2. Hero Section
The hero is the most important section. It must communicate your value proposition
in under 5 seconds.

Layout pattern:

tsx

<section className="relative flex min-h-screen items-center justify-center overflow-hidden pt-16">
  {/* Background effects (gradient, grid, or image) */}
  <div className="absolute inset-0 -z-10">
    {/* Subtle gradient or dot grid */}
  </div>

  <div className="mx-auto max-w-4xl px-6 text-center">
    {/* Badge */}
    <motion.div
      initial={{ opacity: 0, y: 20 }}
      animate={{ opacity: 1, y: 0 }}
      transition={{ duration: 0.5 }}
    >
      <Badge variant="outline" className="mb-6">
        Now in Public Beta
      </Badge>
    </motion.div>

    {/* Heading */}
    <motion.h1
      className="text-5xl font-bold tracking-tight md:text-7xl"
      initial={{ opacity: 0, y: 20 }}
      animate={{ opacity: 1, y: 0 }}
      transition={{ duration: 0.5, delay: 0.1 }}
    >
      Build beautiful products{" "}
      <span className="bg-gradient-to-r from-violet-400 to-pink-400 bg-clip-text text-transparent">
        faster than ever
      </span>
    </motion.h1>

    {/* Subheading */}
    <motion.p
      className="mt-6 text-lg text-muted-foreground md:text-xl"
      initial={{ opacity: 0, y: 20 }}
      animate={{ opacity: 1, y: 0 }}
      transition={{ duration: 0.5, delay: 0.2 }}
    >
      A brief, clear description of what your product does and why it matters.
      Keep it to 1-2 sentences. No jargon.
    </motion.p>

    {/* CTA buttons */}
    <motion.div
      className="mt-10 flex flex-col items-center gap-4 sm:flex-row sm:justify-center"
      initial={{ opacity: 0, y: 20 }}
      animate={{ opacity: 1, y: 0 }}
      transition={{ duration: 0.5, delay: 0.3 }}
    >
      <Button size="lg">Get Started Free</Button>
      <Button variant="outline" size="lg">
        Watch Demo
      </Button>
    </motion.div>
  </div>
</section>
Hero rules:

Heading: 48-72px, bold, tight letter-spacing (-0.03em)
One gradient text span for visual interest (never more than one)
Subheading: 18-20px, muted color, 1-2 sentences maximum
Two CTAs: primary (filled) + secondary (outline)
Generous vertical padding: py-24 to py-32
Badge above heading (optional, but adds context)
Staggered entry animations (100ms delay between elements)
3. Social Proof Bar
tsx

<section className="border-y border-border py-12">
  <div className="mx-auto max-w-6xl px-6">
    <p className="text-center text-sm text-muted-foreground mb-8">
      Trusted by teams at
    </p>
    <div className="flex flex-wrap items-center justify-center gap-x-12 gap-y-6">
      {/* Logo components, rendered in grayscale/muted */}
      {logos.map((logo) => (
        <div key={logo.name} className="opacity-40 grayscale hover:opacity-100 hover:grayscale-0 transition">
          <logo.component className="h-8" />
        </div>
      ))}
    </div>
  </div>
</section>
4. Feature Grid
tsx

<section className="py-24 md:py-32">
  <div className="mx-auto max-w-6xl px-6">
    {/* Section header */}
    <div className="text-center mb-16">
      <h2 className="text-3xl font-bold tracking-tight md:text-4xl">
        Everything you need
      </h2>
      <p className="mt-4 text-lg text-muted-foreground max-w-2xl mx-auto">
        A concise explanation of the value these features provide together.
      </p>
    </div>

    {/* Grid */}
    <div className="grid gap-8 md:grid-cols-2 lg:grid-cols-3">
      {features.map((feature, i) => (
        <motion.div
          key={feature.title}
          initial={{ opacity: 0, y: 20 }}
          whileInView={{ opacity: 1, y: 0 }}
          viewport={{ once: true }}
          transition={{ delay: i * 0.1, duration: 0.5 }}
          className="rounded-2xl border border-border bg-card p-6"
        >
          <div className="mb-4 inline-flex rounded-lg bg-muted p-2">
            <feature.icon className="h-5 w-5" />
          </div>
          <h3 className="text-lg font-semibold">{feature.title}</h3>
          <p className="mt-2 text-sm text-muted-foreground">
            {feature.description}
          </p>
        </motion.div>
      ))}
    </div>
  </div>
</section>
5. Testimonials
tsx

<section className="border-y border-border bg-muted/30 py-24 md:py-32">
  <div className="mx-auto max-w-6xl px-6">
    <h2 className="text-center text-3xl font-bold tracking-tight">
      Loved by developers
    </h2>
    <div className="mt-16 grid gap-6 md:grid-cols-3">
      {testimonials.map((t, i) => (
        <motion.div
          key={i}
          initial={{ opacity: 0, y: 20 }}
          whileInView={{ opacity: 1, y: 0 }}
          viewport={{ once: true }}
          transition={{ delay: i * 0.1 }}
          className="rounded-2xl border border-border bg-card p-6"
        >
          <p className="text-sm leading-relaxed">"{t.quote}"</p>
          <div className="mt-6 flex items-center gap-3">
            <img src={t.avatar} className="h-10 w-10 rounded-full" />
            <div>
              <p className="text-sm font-medium">{t.name}</p>
              <p className="text-xs text-muted-foreground">{t.role}</p>
            </div>
          </div>
        </motion.div>
      ))}
    </div>
  </div>
</section>
6. Final CTA
tsx

<section className="py-24 md:py-32">
  <div className="mx-auto max-w-3xl px-6 text-center">
    <h2 className="text-3xl font-bold tracking-tight md:text-5xl">
      Ready to get started?
    </h2>
    <p className="mt-6 text-lg text-muted-foreground">
      Join thousands of teams already building with [Product].
    </p>
    <div className="mt-10 flex flex-col items-center gap-4 sm:flex-row sm:justify-center">
      <Button size="lg">Start Building Free</Button>
      <Button variant="outline" size="lg">Talk to Sales</Button>
    </div>
  </div>
</section>
Section Spacing Reference
text

Between sections:     py-24 (96px) on mobile, py-32 (128px) on desktop
Within sections:      mb-16 (64px) between header and content
Grid gap:             gap-6 (24px) or gap-8 (32px)
Container padding:    px-6 (24px)
Max width:            max-w-6xl (1152px) or max-w-7xl (1280px)
Background Effects
Premium landing pages use subtle background effects to avoid feeling flat:

Dot grid: Small dots in a regular pattern, very low opacity
Gradient mesh: Multiple radial gradients blended together
Glow: A large, soft radial gradient in the accent color behind the hero
Grid lines: Subtle grid pattern (like graph paper) at very low opacity
Never: Animated background particles, star fields, or complex WebGL scenes
for a product landing page
Anti-Patterns
Hero with more than 3 elements (badge + heading + subheading + 2 buttons is the max)
Feature descriptions longer than 2 sentences
More than 6 features in the main grid (use a "See all features" link for more)
Testimonials without real names and photos
CTA buttons with more than 4 words
Inconsistent section widths or padding
Stock photos that look like stock photos
Auto-playing videos in the hero (optional click-to-play is fine)
