name: modern-component-building
description: >
Build production-ready, premium UI components using React, Next.js, Tailwind CSS, and
Framer Motion. Covers component architecture, animation patterns, composition over
configuration, and the design principles that make components look professional.
Use when building UI components, cards, heroes, testimonials, loaders, or any
interactive UI element that needs to look polished and feel smooth.
Modern Component Building
Overview
Building modern UI components is the core craft of a design engineer. A great component is
not just functional — it is beautiful, accessible, responsive, animated, and composable.
This skill covers the patterns and principles for building components that look and feel
like they belong in a premium product, drawing from the techniques used in Aceternity UI.

Source & Credit: Based on the component-building philosophy and techniques from
Manu Arora's Aceternity UI (ui.aceternity.com), his videos "Let's Rebuild This UI
Component From Scratch", "This UI Component Looks Impossible to Build", and his tutorials
on building loaders, testimonials, and scroll animation components (youtube.com/@manuarora).

When to Use This Skill
Building any UI component (cards, heroes, forms, modals, testimonials, etc.)
User wants a "premium" or "polished" component
Rebuilding or improving an existing component
Creating a reusable component library
User references Aceternity UI or similar component libraries
Component Design Principles
1. Composition Over Configuration
Prefer composition (children/slots) over endless props:

tsx

// BAD: Configuration-heavy
<Card
  title="Hello"
  description="World"
  icon={<Icon />}
  action={<Button>Click</Button>}
  image="/img.png"
  badge="New"
/>

// GOOD: Composition-based
<Card>
  <CardIcon><Icon /></CardIcon>
  <CardContent>
    <CardBadge>New</CardBadge>
    <CardTitle>Hello</CardTitle>
    <CardDescription>World</CardDescription>
  </CardContent>
  <CardAction>
    <Button>Click</Button>
  </CardAction>
</Card>
2. Animations Are Not Optional
Every component that appears or changes state should have a transition. This is what
separates "developer UI" from "design engineer UI."

Minimum animation for every component:

Entry: fade + slight translate (opacity 0→1, y 10→0)
Hover: subtle lift or shadow change (translateY -2px, or box-shadow increase)
Active/press: subtle scale down (scale 0.98)
Exit: reverse of entry (if applicable)
3. The Container Pattern
Most Aceternity UI components use a pattern where a container handles the complex
logic (animation, state, effects) and a simple inner component handles the visual
markup. This keeps components copy-pasteable while encapsulating complexity.

tsx

// Container handles all the complexity
function AnimatedCardContainer({ children, className }: Props) {
  const [mousePosition, setMousePosition] = useState({ x: 0, y: 0 });
  const [isHovered, setIsHovered] = useState(false);

  const handleMouseMove = (e: React.MouseEvent) => {
    const rect = e.currentTarget.getBoundingClientRect();
    setMousePosition({
      x: e.clientX - rect.left,
      y: e.clientY - rect.top,
    });
  };

  return (
    <motion.div
      className={cn("relative overflow-hidden", className)}
      onMouseMove={handleMouseMove}
      onMouseEnter={() => setIsHovered(true)}
      onMouseLeave={() => setIsHovered(false)}
      whileHover={{ y: -4 }}
      transition={{ duration: 0.2 }}
    >
      {/* Gradient spotlight that follows mouse */}
      <div
        className="pointer-events-none absolute -inset-px rounded-xl opacity-0
                    transition duration-300"
        style={{
          background: `radial-gradient(600px circle at ${mousePosition.x}px
                       ${mousePosition.y}px, rgba(255,255,255,0.1), transparent 40%)`,
          opacity: isHovered ? 1 : 0,
        }}
      />
      {children}
    </motion.div>
  );
}

// Simple visual component — easy to customize
function AnimatedCard({ title, description, className }: CardProps) {
  return (
    <AnimatedCardContainer className={cn("rounded-xl border p-6", className)}>
      <h3 className="text-lg font-semibold">{title}</h3>
      <p className="mt-2 text-sm text-muted-foreground">{description}</p>
    </AnimatedCardContainer>
  );
}
4. Glassmorphism and Subtle Depth
Modern premium components often use subtle glass effects:

tsx

// Glass card
<div className="relative overflow-hidden rounded-2xl border border-white/10
                bg-white/5 backdrop-blur-xl p-6">
  {/* Content */}
</div>

// Subtle gradient border (using a wrapper)
<div className="relative rounded-2xl p-[1px] bg-gradient-to-r from-white/20 to-white/5">
  <div className="rounded-2xl bg-black/80 backdrop-blur-xl p-6">
    {/* Content */}
  </div>
</div>
Component Recipes
Premium Card with Hover Glow
tsx

function GlowCard({ children, className }: { children: React.ReactNode; className?: string }) {
  const [hovered, setHovered] = useState(false);
  const [position, setPosition] = useState({ x: 0, y: 0 });

  return (
    <div
      className={cn(
        "relative rounded-2xl border border-white/10 bg-black p-8 overflow-hidden",
        className
      )}
      onMouseEnter={() => setHovered(true)}
      onMouseLeave={() => setHovered(false)}
      onMouseMove={(e) => {
        const rect = e.currentTarget.getBoundingClientRect();
        setPosition({ x: e.clientX - rect.left, y: e.clientY - rect.top });
      }}
    >
      {/* Glow effect */}
      <div
        className="pointer-events-none absolute inset-0 transition-opacity duration-300"
        style={{
          opacity: hovered ? 1 : 0,
          background: `radial-gradient(400px circle at ${position.x}px ${position.y}px,
                       rgba(120, 119, 198, 0.15), transparent 50%)`,
        }}
      />
      {/* Gradient border glow on hover */}
      <div
        className="pointer-events-none absolute -inset-[1px] rounded-2xl transition-opacity
                    duration-300"
        style={{
          opacity: hovered ? 1 : 0,
          background: `radial-gradient(400px circle at ${position.x}px ${position.y}px,
                       rgba(255,255,255,0.2), transparent 50%)`,
        }}
      />
      <div className="relative z-10">{children}</div>
    </div>
  );
}
Smooth Number Counter
tsx

function Counter({ target, duration = 2 }: { target: number; duration?: number }) {
  const [count, setCount] = useState(0);
  const ref = useRef<HTMLSpanElement>(null);

  useEffect(() => {
    const observer = new IntersectionObserver(
      ([entry]) => {
        if (entry.isIntersecting) {
          let start = 0;
          const end = target;
          const increment = end / (duration * 60); // 60fps
          const timer = setInterval(() => {
            start += increment;
            if (start >= end) {
              setCount(end);
              clearInterval(timer);
            } else {
              setCount(Math.floor(start));
            }
          }, 1000 / 60);
          observer.disconnect();
        }
      },
      { threshold: 0.5 }
    );
    if (ref.current) observer.observe(ref.current);
    return () => observer.disconnect();
  }, [target, duration]);

  return <span ref={ref}>{count.toLocaleString()}</span>;
}
Text Gradient Effect
tsx

function GradientText({
  children,
  className,
}: {
  children: React.ReactNode;
  className?: string;
}) {
  return (
    <span
      className={cn(
        "bg-clip-text text-transparent bg-gradient-to-r from-indigo-400 via-purple-400
         to-pink-400",
        className
      )}
    >
      {children}
    </span>
  );
}
Spotlight Cursor Effect
tsx

function SpotlightCard({ children, className }: { children: React.ReactNode; className?: string }) {
  const divRef = useRef<HTMLDivElement>(null);
  const [isFocused, setIsFocused] = useState(false);
  const [position, setPosition] = useState({ x: 0, y: 0 });
  const [opacity, setOpacity] = useState(0);

  const handleMouseMove = (e: React.MouseEvent<HTMLDivElement>) => {
    if (!divRef.current) return;
    const rect = divRef.current.getBoundingClientRect();
    setPosition({ x: e.clientX - rect.left, y: e.clientY - rect.top });
  };

  const handleFocus = () => { setIsFocused(true); setOpacity(1); };
  const handleBlur = () => { setIsFocused(false); setOpacity(0); };

  return (
    <motion.div
      ref={divRef}
      onMouseMove={handleMouseMove}
      onMouseEnter={handleFocus}
      onMouseLeave={handleBlur}
      className={cn("relative overflow-hidden rounded-xl border p-8", className)}
      whileHover={{ y: -2 }}
    >
      <div
        className="pointer-events-none absolute -inset-px rounded-xl opacity-0
                    transition duration-500"
        style={{
          opacity,
          background: `radial-gradient(600px circle at ${position.x}px ${position.y}px,
                       rgba(255,255,255,0.06), transparent 40%)`,
        }}
      />
      {children}
    </motion.div>
  );
}
Tailwind CSS Tips for Premium Components
Border Radius Strategy
css

/* Use consistent radius throughout */
.rounded-sm   /* 4px — tags, badges */
.rounded-md   /* 6px — small buttons */
.rounded-lg   /* 8px — buttons, inputs */
.rounded-xl   /* 12px — cards */
.rounded-2xl  /* 16px — large cards, modals */
.rounded-full /* 9999px — pills, avatars, icon buttons */
Shadow Strategy
css

/* Subtle is always better */
.shadow-sm    /* 0 1px 2px rgba(0,0,0,0.05) — minimal elevation */
.shadow-md    /* 0 4px 6px rgba(0,0,0,0.07) — cards */
.shadow-lg    /* 0 10px 15px rgba(0,0,0,0.1) — modals, dropdowns */
/* Avoid shadow-xl and shadow-2xl for UI elements — too heavy */
Dark Mode Best Practices
css

/* Never use pure black backgrounds */
.bg-[#0A0A0A]  /* Rich dark */
.bg-[#111111]  /* Standard dark */
.bg-[#1A1A1A]  /* Elevated dark (cards on dark bg) */

/* Text on dark backgrounds */
.text-white/90   /* Primary text — slightly muted white */
.text-white/60   /* Secondary text */
.text-white/40   /* Disabled/hint text */
Anti-Patterns
Components that only work in one context (tight coupling to parent layout)
Components without hover/focus/active states
Using !important in component styles
Hardcoding colors instead of using design tokens
Components that do not respect the parent container width
Building animations that run on every render (missing once: true on viewport animations)
Ignoring accessibility (missing aria labels, keyboard navigation, focus rings)
