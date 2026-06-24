
name: premium-ui-animation
description: >
Create smooth, purposeful UI animations that make interfaces feel premium and alive.
Covers CSS transitions, Framer Motion patterns, scroll-triggered animations, and the
micro-interaction techniques used on high-end product websites. Use when building animated
components, adding motion to a page, creating scroll effects, or when the user wants
"smooth animations", "make it feel premium", "add motion", or "polish the interactions".
Premium UI Animation
Overview
Animation in UI is not decoration — it is communication. Good animation guides attention,
provides feedback, creates spatial relationships, and makes interfaces feel responsive and
alive. Bad animation distracts, confuses, and slows down the user. This skill covers the
principles and patterns for creating animations that feel premium, purposeful, and smooth.

Source & Credit: Synthesized from multiple videos by Manu Arora
(youtube.com/@manuarora) including "This Simple UI Animation Trick Makes Your Design Look 10x
Better", "The Most Popular UI/UX Animation Technique", "10 Websites for Insane UI Animations",
and the animation philosophy embedded in Aceternity UI (ui.aceternity.com).

When to Use This Skill
User wants to add animations to a UI
Building scroll-triggered reveals or parallax effects
Creating hover effects, page transitions, or micro-interactions
Making a landing page or product page feel "alive" or "premium"
User asks for "smooth" animations or complains that something "feels janky"
Core Philosophy
The 10x Animation Trick
The single most impactful animation technique is also the simplest: fade up on entry with a
slight delay between sibling elements. This single pattern, applied consistently across a
page, transforms it from static to premium.

css

@keyframes fadeUp {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.animate-in {
  animation: fadeUp 0.6s ease-out forwards;
  opacity: 0;
}
Apply staggered delays: each sibling element gets animation-delay: calc(var(--i) * 100ms).

Animation Purpose Hierarchy
Every animation must serve one of these purposes. If it does not, remove it:

Feedback: Confirming a user action (button press, toggle, form submission)
Orientation: Showing spatial relationships (where did this element come from?)
Focus: Directing attention to what matters (highlight, scale, glow)
Delight: Creating a moment of pleasant surprise (never at the cost of speed)
Continuity: Maintaining context during transitions (shared element, morph)
The "Invisible Animation" Rule
The best animations are the ones the user does not consciously notice. They should feel
natural and expected. If a user thinks "that was a cool animation", it was probably too
much. If they think "that felt smooth", you succeeded.

Framer Motion Patterns for React/Next.js
Fade-Up on Scroll (Viewport Entry)
tsx

import { motion } from "framer-motion";

const fadeUp = {
  hidden: { opacity: 0, y: 20 },
  visible: {
    opacity: 1,
    y: 0,
    transition: { duration: 0.5, ease: "easeOut" },
  },
};

function Section({ children }) {
  return (
    <motion.section
      initial="hidden"
      whileInView="visible"
      viewport={{ once: true, margin: "-100px" }}
      variants={fadeUp}
    >
      {children}
    </motion.section>
  );
}
Staggered Children
tsx

const container = {
  hidden: { opacity: 0 },
  visible: {
    opacity: 1,
    transition: { staggerChildren: 0.1, delayChildren: 0.2 },
  },
};

const item = {
  hidden: { opacity: 0, y: 20 },
  visible: {
    opacity: 1,
    y: 0,
    transition: { duration: 0.5, ease: "easeOut" },
  },
};

function CardGrid({ cards }) {
  return (
    <motion.div
      className="grid grid-cols-3 gap-6"
      variants={container}
      initial="hidden"
      whileInView="visible"
      viewport={{ once: true }}
    >
      {cards.map((card) => (
        <motion.div key={card.id} variants={item}>
          <Card {...card} />
        </motion.div>
      ))}
    </motion.div>
  );
}
Smooth Hover Card
tsx

function PremiumCard({ children, className }) {
  return (
    <motion.div
      className={className}
      whileHover={{ y: -4, transition: { duration: 0.2 } }}
      whileTap={{ scale: 0.98 }}
    >
      {children}
    </motion.div>
  );
}
Page Section Scroll Progress
tsx

import { useScroll, useTransform, motion } from "framer-motion";

function ParallaxSection() {
  const ref = useRef(null);
  const { scrollYProgress } = useScroll({
    target: ref,
    offset: ["start end", "end start"],
  });
  const y = useTransform(scrollYProgress, [0, 1], [100, -100]);

  return (
    <section ref={ref} className="relative overflow-hidden">
      <motion.div style={{ y }}>
        <img src="/hero.png" alt="" className="w-full" />
      </motion.div>
    </section>
  );
}
Scroll-Linked Opacity (Hero Text Fade)
tsx

function FadingHero() {
  const ref = useRef(null);
  const { scrollYProgress } = useScroll({
    target: ref,
    offset: ["start start", "end start"],
  });
  const opacity = useTransform(scrollYProgress, [0, 0.8], [1, 0]);
  const y = useTransform(scrollYProgress, [0, 0.8], [0, 100]);

  return (
    <motion.div ref={ref} style={{ opacity, y }} className="text-center">
      <h1 className="text-6xl font-bold">Premium Heading</h1>
      <p className="text-xl text-gray-500 mt-4">This fades as you scroll</p>
    </motion.div>
  );
}
Timing and Easing Reference
Duration Guidelines
Animation Type
Duration
Easing
Hover state change	150-200ms	ease-out
Button press	100-150ms	ease-in
Tooltip/appear	200-300ms	ease-out
Modal open	300-400ms	[0.32, 0.72, 0, 1] (custom spring)
Page transition	300-500ms	ease-in-out
Scroll reveal	500-800ms	ease-out
Complex orchestration	800-1200ms	custom per element
Loading/looping	1500-3000ms	ease-in-out

Easing Curves
ease-out (0, 0, 0.58, 1) — Default for almost everything. Fast start, slow end.
ease-in-out (0.42, 0, 0.58, 1) — For symmetric transitions (page transitions, toggles).
ease-in — Only for exit animations (things leaving the screen).
Custom spring [0.32, 0.72, 0, 1] — For modal open/close, feels snappy yet smooth.
cubic-bezier(0.16, 1, 0.3, 1) — "Expo out", great for scroll reveals.
Performance Rules
Animate only transform and opacity. These are GPU-accelerated. Animating width,
height, margin, padding, or top/left causes layout thrashing.
Use will-change sparingly — only on elements that will animate, and remove it after.
Respect prefers-reduced-motion — provide static fallbacks for users who prefer
no animation:
css

@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    transition-duration: 0.01ms !important;
  }
}
Use viewport={{ once: true }} on scroll-triggered animations to prevent re-triggering.
Avoid animating box-shadow — it is expensive. Use a pseudo-element with opacity
transition instead.
Anti-Patterns
Bouncing animations (unless for a specific notification purpose)
Rotation animations on page elements (save for loading spinners)
Animating more than 2-3 properties simultaneously
Using animation: infinite for anything except subtle background effects
Making the user wait for an animation before they can interact
Different animation timings for similar elements (inconsistency feels broken)
Parallax on every section (one parallax moment per page is enough)
