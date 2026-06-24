name: scroll-driven-effects
description: >
Build scroll-triggered animations, parallax effects, progress indicators, and
scroll-linked interactions using Framer Motion's useScroll and useTransform hooks.
Covers viewport-triggered reveals, scroll-linked opacity/transform, and the
patterns used on premium product websites. Use when the user wants scroll
animations, parallax, "animate on scroll", or scroll-linked effects.
Scroll-Driven Effects
Overview
Scroll-driven effects are animations that respond to the user's scroll position. When
done well, they create a sense of depth, narrative, and interactivity that makes a
page feel alive. When done poorly, they are distracting and hurt performance. This
skill covers the patterns for building scroll effects that enhance rather than
detract from the user experience.

Source & Credit: Based on scroll animation techniques demonstrated by
Manu Arora in his scroll animation component tutorials and the scroll-driven
effects built into Aceternity UI components (ui.aceternity.com,
youtube.com/@manuarora). Core API patterns from Framer Motion documentation.

When to Use This Skill
Building scroll-triggered reveal animations
Creating parallax effects
Implementing scroll-linked progress bars or indicators
Making elements respond to scroll position (opacity, scale, transform)
Building immersive storytelling pages
Fundamental API: Framer Motion useScroll
tsx

import { useScroll, useTransform, motion, useSpring } from "framer-motion";
import { useRef } from "react";

function ScrollExample() {
  const ref = useRef(null);

  // Track scroll progress of this element
  const { scrollYProgress } = useScroll({
    target: ref,
    offset: ["start end", "end start"],  // When top of element hits bottom of viewport
                                          // until bottom of element hits top of viewport
  });

  // Transform scroll progress (0-1) into any value
  const opacity = useTransform(scrollYProgress, [0, 0.5, 1], [0, 1, 0]);
  const y = useTransform(scrollYProgress, [0, 1], [100, -100]);
  const scale = useTransform(scrollYProgress, [0, 0.5, 1], [0.8, 1, 0.8]);

  return (
    <div ref={ref} className="relative h-[200vh]">
      <motion.div style={{ opacity, y, scale }} className="sticky top-0 h-screen">
        <h1>Scroll to animate me</h1>
      </motion.div>
    </div>
  );
}
Pattern 1: Viewport Entry Reveal
The most common and useful scroll effect — elements fade in as they enter the viewport.

tsx

const revealOnScroll = {
  hidden: { opacity: 0, y: 30 },
  visible: {
    opacity: 1,
    y: 0,
    transition: { duration: 0.6, ease: [0.16, 1, 0.3, 1] },  // "expo out"
  },
};

const staggerContainer = {
  hidden: {},
  visible: {
    transition: { staggerChildren: 0.1 },
  },
};

function FeatureSection() {
  return (
    <motion.section
      variants={staggerContainer}
      initial="hidden"
      whileInView="visible"
      viewport={{ once: true, margin: "-80px" }}
      className="py-24"
    >
      <motion.h2 variants={revealOnScroll} className="text-4xl font-bold">
        Features
      </motion.h2>
      <motion.p variants={revealOnScroll} className="mt-4 text-muted-foreground">
        Description text
      </motion.p>
      <div className="mt-12 grid gap-6 md:grid-cols-3">
        {features.map((f, i) => (
          <motion.div key={i} variants={revealOnScroll} className="card">
            {f.content}
          </motion.div>
        ))}
      </div>
    </motion.section>
  );
}
Key: viewport={{ once: true }} — This prevents the animation from re-triggering
every time the user scrolls back up. Use this for one-shot reveals.

Pattern 2: Scroll-Linked Parallax
Elements move at different speeds relative to scroll, creating depth.

tsx

function ParallaxHero() {
  const ref = useRef(null);
  const { scrollYProgress } = useScroll({
    target: ref,
    offset: ["start start", "end start"],
  });

  // Background moves slower (parallax effect)
  const backgroundY = useTransform(scrollYProgress, [0, 1], ["0%", "30%"]);
  // Text fades out as user scrolls
  const textOpacity = useTransform(scrollYProgress, [0, 0.5], [1, 0]);
  const textY = useTransform(scrollYProgress, [0, 0.5], [0, 100]);

  return (
    <section ref={ref} className="relative h-screen overflow-hidden">
      <motion.div
        className="absolute inset-0 bg-cover bg-center"
        style={{ y: backgroundY }}
      >
        <img src="/hero-bg.jpg" alt="" className="w-full h-full object-cover" />
      </motion.div>
      <motion.div
        className="relative z-10 flex h-full items-center justify-center"
        style={{ opacity: textOpacity, y: textY }}
      >
        <h1 className="text-7xl font-bold text-white">Hero Text</h1>
      </motion.div>
    </section>
  );
}
Pattern 3: Scroll Progress Indicator
A line or bar that shows how far the user has scrolled through a section.

tsx

function ScrollProgressLine() {
  const { scrollYProgress } = useScroll();

  return (
    <motion.div
      className="fixed top-0 left-0 right-0 h-[2px] bg-gradient-to-r from-violet-500 to-pink-500
                 origin-left z-50"
      style={{ scaleX: scrollYProgress }}
    />
  );
}

// Section-specific progress
function SectionProgress({ children, className }: { children: React.ReactNode; className?: string }) {
  const ref = useRef(null);
  const { scrollYProgress } = useScroll({
    target: ref,
    offset: ["start end", "end end"],
  });

  return (
    <section ref={ref} className={className}>
      <motion.div
        className="absolute top-0 left-0 h-full w-[2px] bg-accent origin-top"
        style={{ scaleY: scrollYProgress }}
      />
      {children}
    </section>
  );
}
Pattern 4: Horizontal Scroll Section
Content scrolls horizontally as the user scrolls vertically — popular on portfolio
and storytelling sites.

tsx

function HorizontalScroll({ items }: { items: React.ReactNode[] }) {
  const ref = useRef(null);
  const { scrollYProgress } = useScroll({
    target: ref,
    offset: ["start start", "end end"],
  });

  const x = useTransform(scrollYProgress, [0, 1], ["0%", `-${(items.length - 1) * 100}%`]);

  return (
    <section ref={ref} className="relative h-[300vh]">
      <div className="sticky top-0 h-screen overflow-hidden">
        <motion.div className="flex h-full items-center" style={{ x }}>
          {items.map((item, i) => (
            <div key={i} className="min-w-screen flex items-center justify-center px-12">
              {item}
            </div>
          ))}
        </motion.div>
      </div>
    </section>
  );
}
Pattern 5: Text Reveal on Scroll
Characters or words reveal as the user scrolls through a section.

tsx

function ScrollTextReveal({ text }: { text: string }) {
  const ref = useRef(null);
  const { scrollYProgress } = useScroll({
    target: ref,
    offset: ["start 0.9", "start 0.3"],
  });

  const words = text.split(" ");

  return (
    <p ref={ref} className="text-3xl font-bold leading-relaxed">
      {words.map((word, i) => {
        const start = i / words.length;
        const end = start + 1 / words.length;
        return (
          <Word key={i} range={[start, end]} progress={scrollYProgress}>
            {word}
          </Word>
        );
      })}
    </p>
  );
}

function Word({
  children,
  range,
  progress,
}: {
  children: string;
  range: [number, number];
  progress: MotionValue<number>;
}) {
  const opacity = useTransform(progress, range, [0.2, 1]);
  const color = useTransform(progress, range, ["rgba(255,255,255,0.2)", "rgba(255,255,255,1)"]);
  return (
    <motion.span className="inline-block mr-2" style={{ opacity, color }}>
      {children}
    </motion.span>
  );
}
Performance Guidelines
Prefer whileInView over scroll event listeners — Framer Motion handles this
with IntersectionObserver, which is more performant.
Use will-change: transform only on elements actively being animated.
Avoid scroll-linked animations on many elements simultaneously — limit to 3-5
scroll-linked elements per viewport.
Use useSpring to smooth scroll values and reduce jank:
tsx

const smoothProgress = useSpring(scrollYProgress, {
  stiffness: 100,
  damping: 30,
  restDelta: 0.001,
});
Test on mobile — scroll effects can cause layout thrashing on low-end devices.
Consider reducing or disabling parallax on mobile.
Anti-Patterns
Parallax on every section of a page (one moment per page is enough)
Scroll-jacking (preventing the user from scrolling naturally)
Scroll effects that cause noticeable frame drops
Animations that re-trigger on every scroll (missing once: true)
Content that is unreadable until scrolled to a specific position
Scroll speed that does not match the user's scroll input
More than 2 "scroll surprise" moments per page
