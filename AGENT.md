# AGENT.md - GluonEX Clone with Astro

## Project Context

Clone of [gluonex.cl](https://gluonex.cl) built with Astro. The original site is made with Next.js; this clone aims to replicate the functionality and design but with a **static-first** approach for maximum speed.

**Main objective**: Speed above all. The site must be mostly static files with minimal JavaScript.

## Tech Stack

| Layer      | Technology               | Notes                                     |
| ---------- | ------------------------ | ----------------------------------------- |
| Framework  | Astro 6                  | Static-first, islands architecture        |
| UI Library | DaisyUI + Tailwind CSS 4 | Colors via `globals.css` extracted from logo, never hardcoded |
| Icons      | Lucide                   | Consistency and tree-shaking              |
| Animations | Motion One (~5kb)        | Lightweight alternative to Framer Motion  |
| Forms      | WhatsApp redirect        | No email sending, no backend              |
| Font       | Inter                    | Maintain consistency with original        |

## Architecture

```
src/
├── components/
│   ├── ui/           # Customized DaisyUI base components
│   ├── sections/     # Page sections (Hero, About, Services, Contact, Footer)
│   └── icons/        # Lucide icons wrapper if needed
├── layouts/
│   └── Layout.astro  # Main layout with meta tags, fonts, SEO
├── pages/
│   └── index.astro   # SPA - entire website in one page
├── styles/
│   └── globals.css   # DaisyUI theme + Tailwind customizations
├── assets/
│   └── images/       # Logo, screenshots, etc.
└── lib/
    └── utils.ts      # Shared utilities (if needed)
```

## Code Conventions

### Astro vs React Components

**FUNDAMENTAL RULE**: Use Astro by default. React ONLY when there's interactivity that Astro can't handle.

```astro
---
// Static component → Astro (.astro)
// Example: Header, Footer, service cards, content sections
---

// Interactive component → React (.tsx) with client directive
// Example: Nothing currently (forms are WhatsApp redirects)
// If something interactive is needed in the future:
// <Component client:idle /> or client:visible
```

### Theme and Colors

**NEVER hardcode colors**. Always use DaisyUI or Tailwind variables:

```astro
<!-- ✅ Correct -->
<div class="bg-primary text-primary-content">
<h2 class="text-base-content">

<!-- ❌ Incorrect -->
<div class="bg-[#3245ff] text-white">
<h2 class="text-gray-900">
```

Define theme colors in `globals.css` (extracted from logo):

```css
@import "tailwindcss";
@plugin "daisyui" {
  themes: gluonex --default;
}

@theme {
  --color-primary: #7E95A8;    /* Soft steel blue (from "EX" in logo) */
  --color-secondary: #C9A84C;  /* Champagne gold (from circle ring) */
  --color-accent: #1C1C1C;     /* Dark charcoal (from "Gluon" text) */
  --color-neutral: #1C1C1C;
  /* ... rest of theme */
}
```

**Color mapping from logo:**
- `primary` = Soft steel blue `#7E95A8` - Main brand color, CTAs, icons, accents
- `secondary` = Champagne gold `#C9A84C` - Stats numbers, highlights, decorative elements
- `neutral` / `base-content` = Dark charcoal `#1C1C1C` - Text, footer/contact backgrounds

### Component Structure

```astro
---
// 1. Imports
import { Icon } from 'lucide-react';
import AnotherComponent from './AnotherComponent.astro';

// 2. Props interface (if applicable)
interface Props {
  title: string;
  description?: string;
}

// 3. Component logic
const { title, description } = Astro.props;
---

<!-- 4. HTML template with Tailwind + DaisyUI classes -->
<section class="py-20 bg-base-100">
  <div class="container mx-auto px-4">
    <h2 class="text-4xl font-bold text-base-content">{title}</h2>
  </div>
</section>

<!-- 5. Styles (only if necessary, prefer Tailwind) -->
<style>
  /* Specific styles that can't be done with Tailwind */
</style>
```

### Forms → WhatsApp

All forms are converted to WhatsApp links/redirects with pre-filled text:

```astro
---
const phoneNumber = '56973789128';
const baseMessage = 'Hi GluonEX, I would like to quote a project.';
---

<a
  href={`https://wa.me/${phoneNumber}?text=${encodeURIComponent(baseMessage)}`}
  target="_blank"
  rel="noopener noreferrer"
  class="btn btn-primary"
>
  Contact via WhatsApp
</a>
```

For forms with dynamic fields, use a small vanilla JS script (no React):

```html
<form id="contact-form" class="space-y-4">
  <input
    type="text"
    name="nombre"
    placeholder="Your name"
    class="input input-bordered w-full"
  />
  <input
    type="text"
    name="empresa"
    placeholder="Company"
    class="input input-bordered w-full"
  />
  <textarea
    name="mensaje"
    placeholder="Tell us about your project"
    class="textarea textarea-bordered w-full"
  ></textarea>
  <button type="submit" class="btn btn-primary w-full">
    Send via WhatsApp
  </button>
</form>

<script>
  document.getElementById('contact-form')?.addEventListener('submit', (e) => {
    e.preventDefault();
    const form = e.target as HTMLFormElement;
    const data = new FormData(form);

    const nombre = data.get('nombre') || '';
    const empresa = data.get('empresa') || '';
    const mensaje = data.get('mensaje') || '';

    const text = `Hi GluonEX, I'm ${nombre} from ${empresa}. ${mensaje}`;
    const url = `https://wa.me/56973789128?text=${encodeURIComponent(text)}`;

    window.open(url, '_blank');
  });
</script>
```

## Page Structure (SPA)

The entire website lives in a single `index.astro` page with the following sections:

1. **Header/Nav** - Fixed navigation with links to sections (smooth scroll)
2. **Hero** - Main headline + CTA
3. **Our Essence** - Mission, Vision, stats
4. **Services** - Grid of 6 services with Lucide icons
5. **Contact** - Form redirecting to WhatsApp + contact info
6. **Footer** - Links, copyright, social media

## Detailed Sections

### Header

- Logo (optimized SVG)
- Navigation: Home, About, Services, Contact
- Smooth scroll to each section
- Responsive: hamburger menu on mobile

### Hero

- Headline: "High-level solutions within your reach."
- Subtitle about custom software development
- Two CTAs: "Quote Projects" (WhatsApp) + "Learn Services" (scroll)
- Decorative image (world.png from original)

### Our Essence

- Title: "Architects of your digital growth"
- Tabs or cards: Mission and Vision
- Stats: +3 years, 100% custom development, +3 (projects/clients)

### Services

- Title: "What you need for your digital ecosystem"
- 3x2 grid with:
  - Web Design (icon: `layout`)
  - Software Development (icon: `code`)
  - SEO Optimization (icon: `search`)
  - Web Performance (icon: `zap`)
  - Comprehensive Maintenance (icon: `wrench`)
  - Technology Consulting (icon: `lightbulb`)
- CTA "Learn more" (can expand details or redirect to WhatsApp)

### Contact

- Form with fields: Name, Company, Email, Message
- Submit → WhatsApp with data
- Contact info:
  - Phone: +56 9 7378 9128
  - Email: contacto@gluonex.cl
  - LinkedIn: GluonEX
  - Instagram: @gluonex.cl

### Footer

- Logo + tagline
- Featured services
- Contact information
- Social media
- Copyright © 2026 GLUONEX SPA

## Animations (Motion One)

Use Motion One for scroll entry animations:

```astro
<section class="animate-on-scroll">
  <h2>Animated title</h2>
</section>

<script>
  import { animate, scroll } from 'motion';

  // Simple entry animation
  document.querySelectorAll('.animate-on-scroll').forEach((el) => {
    scroll(animate(el, { opacity: [0, 1], y: [50, 0] }));
  });
</script>
```

**Rule**: Load animations with `client:idle` or inline scripts in Astro components. Don't create React components just for animations.

## SEO and Meta Tags

The Layout must include:

```astro
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>GluonEX | IT Services Agency</title>
  <meta name="description" content="High-level solutions within your reach. Custom software development for SMEs and startups in Chile." />
  <meta property="og:title" content="GluonEX | IT Services Agency" />
  <meta property="og:description" content="Boost your SME or startup with custom software development." />
  <meta property="og:image" content="/og-image.png" />
  <link rel="canonical" href="https://gluonex.cl" />
</head>
```

## Images

- Logo: Optimized SVG (don't use PNG if possible)
- world.png: From original site or recreate as SVG
- Favicon: SVG + ICO
- Lazy loading on non-critical images

## Useful Commands

```bash
# Development
pnpm dev

# Production build
pnpm build

# Production preview
pnpm preview

# Add DaisyUI (if not configured)
pnpm add -D daisyui
```

## Implementation Checklist

- [ ] Configure DaisyUI with custom theme in globals.css
- [ ] Install Lucide (lucide-astro for Astro icons)
- [ ] Install Motion One
- [ ] Create Layout.astro with complete meta tags
- [ ] Create Header with responsive navigation
- [ ] Create Hero section
- [ ] Create Our Essence section (Mission/Vision)
- [ ] Create Services grid
- [ ] Create form → WhatsApp
- [ ] Create Footer
- [ ] Add scroll animations
- [ ] Optimize images
- [ ] Test responsive
- [ ] Test performance (Lighthouse)

## Common Mistakes to Avoid

1. **Don't hardcode colors** - Always use theme variables
2. **Don't use React unnecessarily** - Pure Astro is faster
3. **Don't forget `client:*` directives** - If using React, always specify when to load
4. **Don't use `console.log` in production** - Remove all debug code
5. **Don't ignore SEO** - Meta tags are mandatory
6. **Don't overcomplicate animations** - Motion One is simple, don't over-engineer

## Visual Reference

The original gluonex.cl site uses:

- White/light gray background
- Dark text (#1C1C1C)
- Soft steel blue `#7E95A8` for primary accents and CTAs
- Champagne gold `#C9A84C` for stats and highlights
- Blue→gold gradients for card hover effects
- Cards with subtle shadows
- Clean typography with Inter
- Lucide icons (replacing Material Icons)
- Centered layout with max-width

Colors extracted directly from the logo:
- "Gluon" text: Dark charcoal
- "EX" text: Soft steel blue
- Circle ring: Champagne gold
