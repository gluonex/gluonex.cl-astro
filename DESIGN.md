# DESIGN.md - GluonEX Design System

> Single source of truth for visual design. Any AI generating new pages/components for this project MUST follow these patterns exactly.

---

## 1. Brand Identity

| Element | Value |
|---------|-------|
| Company Name | GLUONEX |
| Logo File | `/logo-160.webp` (159x40px display) |
| Favicon | `/icon.png` |
| Tagline | "Arquitectos de tu crecimiento digital" |
| Language | Spanish (lang="es") |

---

## 2. Color Palette

All colors defined in `src/styles/globals.css`. **NEVER hardcode hex values** in components.

### Primary Colors

| Token | Hex | Usage |
|-------|-----|-------|
| `primary` | `#a99b73` | Gold - CTAs, icons, accent text, badges, hover highlights |
| `secondary` | `#475a68` | Slate blue - Secondary CTAs, dark panels, text accent in hero |
| `accent` / `neutral` / `base-content` | `#1c1c1c` | Near-black - Body text, footer bg, dark backgrounds |

### Background Colors

| Token | Hex | Usage |
|-------|-----|-------|
| `base-100` / `surface` | `#ffffff` | White - Main background, cards |
| `base-200` | `#f5f5f5` | Light gray - Alternate section backgrounds |
| `base-300` | `#e5e5e5` | Medium gray - Borders, dividers, input borders |

### Utility Colors

| Token | Hex | Usage |
|-------|-----|-------|
| `muted-foreground` | `#6b6b6b` | Muted/secondary text |
| `outline` | `#d4d4d4` | Outline borders |
| `tertiary` | `#e5e5e5` | Same as base-300, used for subtle borders |

### Color Usage Rules

```
Text on white bg    → text-base-content (#1c1c1c)
Text on dark bg     → text-white
Muted text          → text-base-content/60 or text-base-content/50
Accent text         → text-primary (gold)
Highlighted text    → text-secondary (slate)
CTA buttons         → bg-secondary text-white (primary action)
                     → bg-white border text-secondary (secondary action)
Badges              → bg-primary/10 text-primary
```

---

## 3. Typography

**Font**: Inter (100-900 weight), self-hosted woff2 at `/fonts/inter-latin.woff2`

### Type Scale

| Element | Classes | Use Case |
|---------|---------|----------|
| **Hero H1** | `text-5xl md:text-7xl lg:text-8xl font-extrabold leading-[1.05] tracking-tighter` | Main hero headline |
| **Section H2** | `text-3xl md:text-5xl font-bold tracking-tight` | Section titles |
| **Card H3** | `text-xl md:text-2xl font-bold` | Card headings, subsection titles |
| **Subtitle** | `text-base md:text-xl font-medium` | Hero subtitle, descriptions |
| **Body** | `text-sm md:text-base leading-relaxed` | Paragraph text |
| **Body Large** | `text-base md:text-lg leading-snug` | Quote text, important body |
| **Label/Badge** | `text-[10px] md:text-xs font-bold tracking-widest uppercase` | Section labels, badges |
| **Stat Number** | `text-5xl md:text-6xl font-light text-secondary` | Big numbers (+3, 100%) |
| **Stat Label** | `text-xs md:text-sm font-medium uppercase tracking-wider` | Stat descriptions |
| **Footer Heading** | `text-xs font-bold uppercase tracking-widest` | Footer column titles |
| **Footer Text** | `text-sm leading-relaxed` | Footer body text |
| **Copyright** | `text-xs tracking-wider` | Bottom copyright line |

### Font Weights Used

- `font-extrabold` (800) - Hero H1 only
- `font-bold` (700) - H2, H3, labels, buttons, badges
- `font-semibold` (600) - Nav links, mobile nav links
- `font-medium` (500) - Subtitles, body text, stat labels
- `font-normal` (400) - Default body
- `font-light` (300) - Stat numbers only

---

## 4. Spacing System

### Section Spacing

```
Section padding:     py-20 md:py-32
Section with less:   py-16 md:py-32
```

### Container

```
Standard:    max-w-7xl mx-auto px-6 lg:px-12
Narrow:      max-w-4xl mx-auto
Wide:        max-w-2xl
Form:        container mx-auto px-4 sm:px-6 md:px-12
```

### Component Spacing

```
Card padding (small):    p-8 md:p-10
Card padding (large):    p-6 sm:p-10 md:p-16 lg:p-20
Grid gap (cards):        gap-6 md:gap-8
Grid gap (columns):      gap-12 lg:gap-20
Heading mb (small):      mb-6
Heading mb (medium):     mb-8
Heading mb (large):      mb-12
Heading mb (xlarge):     mb-16 md:mb-20
Item spacing:            space-y-4 or space-y-8
```

---

## 5. Border & Radius

```
Cards:          rounded-3xl
Large cards:    rounded-[3rem] or md:rounded-[3rem]
Small elements: rounded-xl, rounded-2xl
Buttons:        rounded-xl
Badges:         rounded-full
Input fields:   No radius (border-b only)
Icon boxes:     rounded-xl or rounded-2xl
```

### Border Colors

```
Card borders:       border border-base-300
Section dividers:   border-t border-base-300
Input borders:      border-b border-base-300
Hover cards:        hover:border-transparent
```

---

## 6. Shadows

```
Card default:       shadow-sm
Card hover:         hover:shadow-md
Primary CTA:        shadow-2xl
Secondary CTA:      (none, uses border)
Large card:         shadow-[0_80px_100px_-30px_rgba(71,90,104,0.12)]
Quote card:         shadow-[0_8px_32px_0_rgba(0,0,0,0.08),inset_0_1px_1px_rgba(255,255,255,0.4)]
Form submit btn:    shadow-xl
```

---

## 7. Component Patterns

### 7.1 Badge / Tag

```astro
<span class="inline-block bg-primary/10 text-primary px-4 py-1.5 rounded-full text-[10px] md:text-xs font-bold tracking-widest uppercase mb-6">
  Label Text
</span>

<!-- Variant with border -->
<span class="inline-block px-4 py-1.5 rounded-full bg-primary/10 text-primary font-bold tracking-widest text-xs uppercase mb-6 border border-primary/20">
  Label Text
</span>
```

### 7.2 Section Header

```astro
<div class="max-w-2xl">
  <span class="text-primary font-bold tracking-widest text-xs md:text-sm uppercase mb-4 block">
    Section Label
  </span>
  <h2 class="text-3xl md:text-5xl font-bold text-base-content tracking-tight">
    Section Title Goes Here.
  </h2>
</div>
```

### 7.3 Service Card

```astro
<div class="relative bg-white border border-base-300 hover:border-transparent p-8 md:p-10 rounded-3xl group hover:bg-primary/5 transition-all duration-500 shadow-sm hover:shadow-md animate-on-scroll">
  <!-- Gradient border on hover -->
  <div class="absolute inset-0 rounded-3xl opacity-0 group-hover:opacity-100 transition-opacity duration-500 pointer-events-none"
       style="padding:2px;background:linear-gradient(to bottom right, var(--color-primary), var(--color-secondary));-webkit-mask:linear-gradient(#fff 0 0) content-box, linear-gradient(#fff 0 0);-webkit-mask-composite:xor;mask-composite:exclude">
  </div>
  <!-- Icon box -->
  <div class="w-12 h-12 md:w-16 md:h-16 bg-primary/10 rounded-2xl flex items-center justify-center mb-8 group-hover:bg-primary/20 transition-colors">
    <Icon class="w-7 h-7 md:w-8 md:h-8 text-primary" />
  </div>
  <!-- Title -->
  <h3 class="text-xl md:text-2xl font-bold text-base-content mb-4 transition-colors">
    Card Title
  </h3>
  <!-- Description -->
  <p class="text-sm md:text-base text-base-content/60 leading-relaxed transition-colors">
    Card description text goes here.
  </p>
</div>
```

### 7.4 CTA Button - Primary

```astro
<a href="#action" class="relative group bg-secondary text-white px-6 md:px-10 py-3 md:py-5 rounded-xl text-base md:text-lg font-bold shadow-2xl hover:scale-105 transition-transform">
  <span class="relative z-10">Button Text</span>
</a>
```

### 7.5 CTA Button - Secondary

```astro
<a href="#action" class="relative group bg-white border border-base-300 hover:border-transparent px-6 md:px-10 py-3 md:py-5 rounded-xl text-base md:text-lg font-bold hover:bg-base-200 transition-all text-secondary">
  <span class="relative z-10">Button Text</span>
</a>
```

### 7.6 Contact Info Row (Dark Panel)

```astro
<a href="https://..." class="group flex gap-6 items-start hover:bg-white/5 p-3 rounded-2xl transition-colors border border-transparent hover:border-white/10">
  <div class="w-12 h-12 bg-white/10 border border-white/20 rounded-xl flex items-center justify-center shrink-0 group-hover:border-white/40 transition-colors">
    <Icon class="w-5 h-5 text-white" />
  </div>
  <div>
    <p class="text-xs md:text-sm uppercase font-bold text-white/60 tracking-widest mb-1">Label</p>
    <p class="text-lg md:text-xl font-medium text-white">Value</p>
  </div>
</a>
```

### 7.7 Form Input

```astro
<div class="space-y-2">
  <label class="text-sm font-bold text-base-content uppercase tracking-widest">
    Field Label
  </label>
  <input
    class="w-full bg-white border-b border-base-300 p-4 transition-all text-base-content focus:border-primary focus:outline-none"
    placeholder="Placeholder text"
    type="text"
    name="fieldname"
  />
</div>
```

### 7.8 Form Submit Button

```astro
<button class="cursor-pointer relative group bg-secondary text-white w-full py-5 rounded-xl text-lg font-bold shadow-xl hover:bg-primary/90 transition-all" type="submit">
  <span class="relative z-10">Enviar Mensaje</span>
</button>
```

### 7.9 Stats Display

```astro
<div>
  <div class="text-5xl md:text-6xl font-light text-secondary mb-2">+3</div>
  <div class="text-xs md:text-sm font-medium text-base-content/50 uppercase tracking-wider">Label</div>
</div>
```

### 7.10 Quote Card (Glass Effect)

```astro
<div class="absolute -bottom-6 -right-2 md:-bottom-12 md:-right-8 z-20 bg-white/70 p-6 md:p-8 rounded-2xl shadow-[0_8px_32px_0_rgba(0,0,0,0.08),inset_0_1px_1px_rgba(255,255,255,0.4)] backdrop-blur-xl border border-white/50 max-w-[16rem] md:max-w-xs">
  <p class="text-base-content font-medium text-base md:text-lg leading-snug">
    "Quote text here."
  </p>
</div>
```

### 7.11 Footer Section

```astro
<footer class="relative bg-base-content border-t border-white/10 overflow-hidden">
  <div class="container mx-auto px-6 md:px-12 py-20 relative z-10">
    <div class="grid grid-cols-1 md:grid-cols-12 gap-12 text-sm leading-relaxed text-white/50">
      <!-- Column 1: Brand -->
      <div class="md:col-span-12 lg:col-span-5">
        <span class="text-2xl font-bold text-white mb-6 block tracking-tighter">BRAND</span>
        <p class="max-w-sm text-base text-white/60">Tagline text.</p>
      </div>
      <!-- Column 2: Links -->
      <div class="md:col-span-6 lg:col-span-3 lg:col-start-7">
        <h4 class="font-bold text-white mb-6 uppercase tracking-widest text-xs">Title</h4>
        <ul class="space-y-4">
          <li><a href="..." class="hover:text-primary transition-colors">Link</a></li>
        </ul>
      </div>
      <!-- Column 3: Info -->
      <div class="md:col-span-6 lg:col-span-3">
        <h4 class="font-bold text-white mb-6 uppercase tracking-widest text-xs">Info</h4>
        <!-- contact items -->
      </div>
    </div>
  </div>
  <!-- Copyright -->
  <div class="border-t border-white/5 py-8 relative z-10">
    <div class="container mx-auto px-6 md:px-12 flex flex-col items-center justify-center text-xs">
      <div class="text-white/50 tracking-wider text-center">&copy; 2026 BRAND. ALL RIGHTS RESERVED.</div>
    </div>
  </div>
</footer>
```

---

## 8. Layout Patterns

### 8.1 Standard Section

```astro
<section id="section-id" class="py-20 md:py-32 bg-surface relative overflow-hidden">
  <!-- Background effects (optional) -->
  <div class="absolute inset-0 z-0 pointer-events-none">
    <div class="absolute top-1/4 left-0 w-96 h-96 bg-primary/10 rounded-full blur-[100px] -translate-x-1/2"></div>
  </div>
  <!-- Content -->
  <div class="container mx-auto px-6 lg:px-12 relative z-10">
    <!-- Content here -->
  </div>
</section>
```

### 8.2 Section Background Alternation

```
Hero:      bg-surface (white)
About:     bg-base-200 (light gray)
Services:  bg-surface (white)
Contact:   bg-base-200 (light gray)
Footer:    bg-base-content (dark)
```

### 8.3 Grid Layouts

```
2 columns:    grid-cols-1 lg:grid-cols-2
3 columns:    grid-cols-1 md:grid-cols-2 lg:grid-cols-3
12-col grid:  grid-cols-1 lg:grid-cols-12
  5/7 split:  lg:col-span-5 + lg:col-span-7
```

---

## 9. Visual Effects

### 9.1 Background Blurred Orbs

```astro
<div class="absolute top-1/4 -left-32 w-96 h-96 bg-primary/10 rounded-full blur-[100px] animate-[pulse_6s_ease-in-out_infinite]"></div>
<div class="absolute bottom-1/4 -right-32 w-160 h-160 bg-secondary/10 rounded-full blur-[120px] animate-[pulse_8s_ease-in-out_infinite_alternate]"></div>
```

### 9.2 Radial Gradient Dots Pattern

```astro
<div class="absolute inset-0 bg-[radial-gradient(var(--color-primary)_1px,transparent_1px)] bg-size-[40px_40px] opacity-[0.05]"></div>
```

### 9.3 Gradient Border on Hover (Service Cards)

```css
/* Applied via inline style */
padding: 2px;
background: linear-gradient(to bottom right, var(--color-primary), var(--color-secondary));
-webkit-mask: linear-gradient(#fff 0 0) content-box, linear-gradient(#fff 0 0);
-webkit-mask-composite: xor;
mask-composite: exclude;
```

### 9.4 Section Divider Line

```astro
<div class="absolute top-0 inset-x-0 h-px bg-linear-to-r from-transparent via-primary/20 to-transparent"></div>
```

---

## 10. Animation System

### Scroll Reveal

```astro
<!-- Add class to any element -->
<div class="animate-on-scroll">
  Content to reveal
</div>
```

**Script** (in `index.astro`):

```js
import { animate } from "motion";

const observer = new IntersectionObserver(
  (entries) => {
    entries.forEach((entry) => {
      if (entry.isIntersecting) {
        animate(
          entry.target,
          { opacity: [0, 1], y: [20, 0] },
          { duration: 0.8, easing: "ease-out" }
        );
        observer.unobserve(entry.target);
      }
    });
  },
  { threshold: 0.1 }
);

document.querySelectorAll(".animate-on-scroll").forEach((el) => {
  el.style.opacity = "0";
  observer.observe(el);
});
```

---

## 11. Responsive Design

### Breakpoints

```
Mobile:    default (0px+)
Tablet:    md: (768px+)
Desktop:   lg: (1024px+)
```

### Common Responsive Patterns

```
Typography:     text-3xl md:text-5xl lg:text-8xl
Padding:        py-20 md:py-32
Grid:           grid-cols-1 md:grid-cols-2 lg:grid-cols-3
Container:      px-6 lg:px-12
Hidden:         hidden lg:flex (desktop nav)
Show:           lg:hidden (mobile menu toggle)
```

---

## 12. Do's and Don'ts

### DO

- Use semantic color tokens (`text-primary`, `bg-base-200`)
- Add responsive prefixes to ALL visual properties
- Add `animate-on-scroll` to sections for reveal animation
- Use `relative z-10` on content containers above background effects
- Use `pointer-events-none` on decorative background elements
- Use `loading="eager"` and `fetchpriority="high"` on LCP images (hero/about)

### DON'T

- Hardcode hex colors in components (`bg-[#a99b73]` is forbidden)
- Use font sizes without responsive variants
- Skip the gradient border hover effect on cards
- Use React when Astro components suffice
- Forget `overflow-hidden` on sections with background blurs
- Use `console.log` in production scripts
