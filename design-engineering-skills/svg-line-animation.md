name: svg-line-animation
description: >
Create smooth, premium SVG line/path drawing animations using stroke-dasharray and
stroke-dashoffset. Build animated SVG paths, interactive line art, and hand-drawn style
effects. Use when the user asks for SVG animation, line drawing effects, path animation,
animated icons, or wants smooth stroke-based animations.
SVG Line Animation
Overview
SVG line animation is the technique of animating the stroke of SVG paths to create drawing
effects, where lines appear to draw themselves on screen. This creates one of the most visually
satisfying and premium-feeling animations possible on the web. The core mechanism relies on
two CSS/SVG properties: stroke-dasharray and stroke-dashoffset.

Source & Credit: Based on techniques taught by Manu Arora in "The Smoothest SVG
Animation You'll Ever Build" (youtube.com/@manuarora) and the foundational CSS-Tricks guide
on SVG line animation (css-tricks.com/svg-line-animation-works).

When to Use This Skill
User wants animated SVG icons or illustrations
Building a "drawing" effect where lines appear to trace themselves
Creating interactive hover effects on SVG paths
Recreating line art animations seen on premium sites (like joinvalley.com)
Adding sophisticated micro-interactions to buttons, logos, or decorative elements
Core Technique
The Three-Step Mechanism
Step 1: Get the path length

javascript

const path = document.querySelector('.animated-path');
const length = path.getTotalLength();
Step 2: Set dasharray and dashoffset to the full length

This makes the entire stroke appear as a single "dash" that covers the whole path,
then offsets it so the path becomes invisible:

css

.animated-path {
  stroke-dasharray: 1000;  /* must be >= path length */
  stroke-dashoffset: 1000; /* hides the stroke completely */
}
Step 3: Animate stroke-dashoffset to 0

css

.animated-path {
  animation: draw 2s ease-in-out forwards;
}

@keyframes draw {
  to {
    stroke-dashoffset: 0;
  }
}
When stroke-dashoffset reaches 0, the full dash becomes visible — the path appears
to draw itself.

With Framer Motion (React/Next.js)
tsx

import { motion } from "framer-motion";
import { useEffect, useRef } from "react";

function AnimatedPath() {
  const pathRef = useRef<SVGPathElement>(null);

  useEffect(() => {
    if (pathRef.current) {
      const length = pathRef.current.getTotalLength();
      pathRef.current.style.strokeDasharray = `${length}`;
      pathRef.current.style.strokeDashoffset = `${length}`;
    }
  }, []);

  return (
    <motion.path
      ref={pathRef}
      d="M10 80 C 40 10, 65 10, 95 80 S 150 150, 180 80"
      stroke="currentColor"
      strokeWidth={2}
      fill="none"
      animate={{ strokeDashoffset: 0 }}
      transition={{ duration: 2, ease: "easeInOut" }}
    />
  );
}
Interactive Hover Effect (Mouse-Following Draw)
For premium interactive effects where the path draws based on mouse position:

tsx

function InteractiveLine() {
  const pathRef = useRef<SVGPathElement>(null);
  const [length, setLength] = useState(0);

  useEffect(() => {
    if (pathRef.current) {
      setLength(pathRef.current.getTotalLength());
    }
  }, []);

  const handleMouseMove = (e: React.MouseEvent<SVGSVGElement>) => {
    if (!pathRef.current) return;
    const svg = e.currentTarget;
    const rect = svg.getBoundingClientRect();
    const x = e.clientX - rect.left;
    const progress = x / rect.width;
    pathRef.current.style.strokeDashoffset = `${length * (1 - progress)}`;
  };

  return (
    <svg onMouseMove={handleMouseMove} className="w-full h-full">
      <motion.path
        ref={pathRef}
        d="M0 50 Q 250 0, 500 50 T 1000 50"
        stroke="white"
        strokeWidth={1.5}
        fill="none"
        initial={{ strokeDashoffset: length }}
      />
    </svg>
  );
}
Best Practices
Path Quality
Use smooth curves (Q, C, S commands) — jagged polylines with L commands look bad
Simplify paths — fewer control points = smoother animation
Avoid very short segments — they create choppy animations
Test at actual size — paths that look good large may look bad small
Performance
Use will-change: stroke-dashoffset sparingly and only during animation
Prefer CSS animations over JavaScript for simple draw-on-load effects
Use Framer Motion's useMotionValue and useTransform for scroll-driven animations
instead of scroll event listeners
Limit the number of simultaneously animating SVG paths (keep under 20)
Visual Quality
Stroke width: Use thin strokes (1-2px) for elegance. Thick strokes (3px+) look heavy.
Stroke color: Use the accent color or a muted version of it
Line cap: Set strokeLinecap="round" for softer endpoints
Timing: Use ease-in-out for draw effects. Linear feels robotic.
Duration: 1.5-3 seconds for full draw. Shorter feels rushed, longer feels slow.
Advanced: Multiple Path Stagger
For complex illustrations with multiple paths, stagger the animations:

tsx

function StaggeredIcon() {
  const paths = ["M...", "M...", "M..."]; // Your path data
  return (
    <svg viewBox="0 0 100 100">
      {paths.map((d, i) => (
        <motion.path
          key={i}
          d={d}
          stroke="currentColor"
          strokeWidth={1.5}
          fill="none"
          initial={{ pathLength: 0 }}
          animate={{ pathLength: 1 }}
          transition={{
            duration: 1.5,
            delay: i * 0.3,
            ease: "easeInOut",
          }}
        />
      ))}
    </svg>
  );
}
Note: Framer Motion's pathLength prop simplifies this — it normalizes the path
length to 0-1, eliminating the need to manually calculate getTotalLength().

Common Pitfalls
Dasharray too small: If stroke-dasharray is less than the path length, you will
see visible dashes instead of a smooth draw effect. Always use a value >= total length.
Not setting fill="none": The default SVG fill is black, which will cover the
stroke animation. Always set fill="none" on paths you want to animate.
Forgetting forwards: Without animation-fill-mode: forwards, the path will
snap back to its hidden state after the animation completes.
Path not animating smoothly: Ensure the path is a single continuous <path> element,
not a group of disconnected segments.
Cross-browser issues: getTotalLength() works on <path> elements in all modern
browsers. For <line>, <circle>, <rect>, etc., convert them to path data first.
Real-World Reference
This technique was popularized by sites like joinvalley.com and is used extensively in
premium landing pages. The Valley-inspired animation creates a flowing, organic line that
responds to user interaction, making the page feel alive and handcrafted.
