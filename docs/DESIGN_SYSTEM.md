# Eden Portal Design System

> **Version:** 2.0 (with Frontend-Design Skill integration)
> **Last Updated:** 20 January 2026

---

## Quick Reference

| Element | Value |
|---------|-------|
| **Primary colour** | Eden Green `#2d5f4d` |
| **Background** | Eden Mint `#f4f7f6` |
| **Surface** | White `#ffffff` |
| **Display font** | Fraunces |
| **Body font** | DM Sans |
| **Border radius** | 12px (cards), 8px (buttons), 16px (panels) |
| **Animation easing** | `cubic-bezier(0.23, 1, 0.32, 1)` |

---

## Colour Palette

### Core Colours (Eden Calm)

| Name | Hex | CSS Variable | Usage |
|------|-----|--------------|-------|
| Eden White | `#FFFFFF` | `--eden-white` | Card backgrounds, surfaces |
| Eden Mint | `#f4f7f6` | `--eden-mint` | Page backgrounds, subtle fills |
| Eden Green | `#2d5f4d` | `--eden-green` | Primary actions, headings, accents |
| Eden Green Light | `#3d7a63` | `--eden-green-light` | Secondary text, hover states |
| Eden Green Dark | `#1e4435` | `--eden-green-dark` | Active states, emphasis |

### Extended Palette (UI States)

| Name | Hex | CSS Variable | Usage |
|------|-----|--------------|-------|
| Eden Amber | `#d4a156` | `--eden-amber` | Soft warnings (not alarming) |
| Eden Amber Light | `#f5e6cc` | `--eden-amber-light` | Warning backgrounds |
| Eden Rose | `#c27171` | `--eden-rose` | Attention needed (still gentle) |
| Eden Rose Light | `#f5e0e0` | `--eden-rose-light` | Alert backgrounds |
| Eden Sage | `#8ba888` | `--eden-sage` | Success, healthy states |

### Glassmorphism Values

```css
:root {
    --glass-bg: rgba(255, 255, 255, 0.7);
    --glass-border: rgba(45, 95, 77, 0.1);
    --glass-blur: 12px;
    --glass-shadow: 0 8px 32px rgba(45, 95, 77, 0.08);
}
```

### What NOT to Use

- **Grey** — Never use `#808080`, `gray`, `grey` or similar. Use green-tinted neutrals instead.
- **Pure black** — Use `--eden-green-dark` for darkest text
- **Blue for links** — Use `--eden-green` for interactive elements
- **Red for errors** — Use `--eden-rose` (softer, less alarming)

---

## Typography

### Font Stack

```css
:root {
    --font-display: 'Fraunces', Georgia, serif;
    --font-body: 'DM Sans', system-ui, sans-serif;
}
```

### Google Fonts Import

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=DM+Sans:ital,opsz,wght@0,9..40,300;0,9..40,400;0,9..40,500;1,9..40,400&family=Fraunces:ital,opsz,wght@0,9..144,300;0,9..144,400;0,9..144,500;1,9..144,300&display=swap" rel="stylesheet">
```

### Type Scale

| Element | Font | Size | Weight | Line Height |
|---------|------|------|--------|-------------|
| Page title | Fraunces | 1.75rem | 400 | 1.3 |
| Card title | Fraunces | 1.1rem | 400 | 1.4 |
| Body text | DM Sans | 0.875rem | 400 | 1.6 |
| Small text | DM Sans | 0.75rem | 400 | 1.5 |
| Labels | DM Sans | 0.7rem | 500 | 1.4 |
| Buttons | DM Sans | 0.8rem | 500 | 1 |

### Typography Rules

1. **Never use Inter, Roboto, or Arial** — These are "AI slop" fonts
2. **Maximum 2 font families** — Fraunces for display, DM Sans for everything else
3. **Always specify fallbacks** — Georgia for Fraunces, system-ui for DM Sans
4. **Letter spacing for labels** — Use `0.08em` for uppercase category labels

---

## Spacing

### Scale

```css
:root {
    --space-xs: 0.25rem;   /* 4px */
    --space-sm: 0.5rem;    /* 8px */
    --space-md: 1rem;      /* 16px */
    --space-lg: 1.5rem;    /* 24px */
    --space-xl: 2rem;      /* 32px */
    --space-2xl: 3rem;     /* 48px */
}
```

### Usage Guidelines

| Context | Spacing |
|---------|---------|
| Inside buttons | `--space-sm` vertical, `--space-md` horizontal |
| Card padding | `--space-lg` |
| Between cards | `--space-md` |
| Section margins | `--space-xl` |
| Page padding | `--space-xl` (desktop), `--space-md` (mobile) |

---

## Animation

### Timing Variables

```css
:root {
    --ease-out-soft: cubic-bezier(0.23, 1, 0.32, 1);
    --duration-fast: 150ms;
    --duration-normal: 300ms;
    --duration-slow: 500ms;
}
```

### Animation Patterns

#### Card Reveal (Staggered)

```css
.friction-card {
    opacity: 0;
    transform: translateY(12px);
    animation: cardReveal var(--duration-slow) var(--ease-out-soft) forwards;
}

.friction-card:nth-child(1) { animation-delay: 0.1s; }
.friction-card:nth-child(2) { animation-delay: 0.2s; }
.friction-card:nth-child(3) { animation-delay: 0.3s; }

@keyframes cardReveal {
    to {
        opacity: 1;
        transform: translateY(0);
    }
}
```

#### Pulse Indicator

```css
.pulse-indicator {
    width: 6px;
    height: 6px;
    border-radius: 50%;
    background: var(--eden-green);
    animation: pulse 2s ease-in-out infinite;
}

@keyframes pulse {
    0%, 100% { opacity: 1; transform: scale(1); }
    50% { opacity: 0.5; transform: scale(0.85); }
}
```

#### Hover Lift

```css
.card:hover {
    transform: translateY(-2px);
    box-shadow: 0 12px 40px rgba(45, 95, 77, 0.12);
    transition: all var(--duration-normal) var(--ease-out-soft);
}
```

### Motion Principles

1. **Calm over exciting** — No bounce, no elastic, no jarring
2. **Purposeful** — Every animation communicates something
3. **Performant** — Test on mobile, respect `prefers-reduced-motion`
4. **Consistent** — Use the timing variables, don't invent new ones

---

## Components

### Friction Card

The primary UI element for displaying items needing attention.

```
+-------------------------------------------+
|* CATEGORY              2 days             |  <- Header with pulse + time
|                                           |
|  Card Title Here                          |  <- Fraunces, 1.1rem
|  Description text explaining what         |  <- DM Sans, 0.875rem
|  needs attention and why.                 |
|                                           |
|  +------+                                 |
|  | JA   |  Dr. Jane Akintola             |  <- Associate (if relevant)
|  +------+  Associate Therapist            |
|                                           |
|  +-------------+  +-------------+         |
|  |  Primary    |  |  Secondary  |         |  <- Action buttons
|  +-------------+  +-------------+         |
+-------------------------------------------+
```

**Left accent bar colours:**
- Default (info): `--eden-green`
- Attention: `--eden-amber`
- Urgent: `--eden-rose`

### Garden in Bloom (All-Clear State)

Displayed when Friction Feed is empty.

```
         +---------+
         |   leaf  |  <- Animated leaf SVG (draws in)
         +---------+

      Garden in bloom

   Everything is tended. Your
   practice is flowing smoothly.
```

**Typography:**
- Title: Fraunces, 1.5rem, `--eden-green`
- Message: DM Sans, 0.9rem, `--eden-green-light`

---

## Responsive Behaviour

### Breakpoints

| Name | Min Width | Layout |
|------|-----------|--------|
| Mobile | 0px | Single column, Bottom Sheet panels |
| Tablet | 768px | Two columns, Side Panel available |
| Desktop | 1024px | Three columns, Side Panel default |

### Adaptive Components

| Component | Mobile | Desktop |
|-----------|--------|---------|
| Detail panels | Bottom Sheet (slide up) | Side Panel (slide right) |
| Card grid | 1 column | 3 columns |
| Navigation | Hamburger menu | Visible sidebar |
| Padding | `--space-md` | `--space-xl` |

---

## Accessibility

### Colour Contrast (WCAG AA)

| Combination | Ratio | Status |
|-------------|-------|--------|
| Eden Text on White | 12.5:1 | Pass |
| Eden Text on Mint | 11.8:1 | Pass |
| White on Eden Green | 7.2:1 | Pass |

### Focus States

```css
:focus-visible {
    outline: 2px solid var(--eden-green);
    outline-offset: 2px;
}
```

### Touch Targets

Minimum: 44px x 44px

### Reduced Motion

```css
@media (prefers-reduced-motion: reduce) {
    *, *::before, *::after {
        animation-duration: 0.01ms !important;
        transition-duration: 0.01ms !important;
    }
}
```

---

## Anti-Patterns (What NOT to Do)

### Typography
- Using Inter, Roboto, Arial, or generic sans-serif
- More than 2 font families
- Missing font fallbacks

### Colour
- Grey (`#808080`, `gray`, `grey`)
- Pure black (`#000000`)
- Saturated red for errors
- Blue for interactive elements

### Animation
- Bounce or elastic easing
- Animations longer than 500ms for UI
- Decorative animation without purpose
- Ignoring `prefers-reduced-motion`

### Layout
- Traditional dashboards with many metrics
- Dense, cluttered information display
- Clinical white/blue colour schemes
- Generic SaaS aesthetic

---

## Reference

### Anthropic Frontend-Design Skill

Location: `/mnt/skills/public/frontend-design/SKILL.md`

Key principles we adapted:
- Distinctive typography (not generic fonts)
- Intentional motion (meaningful, not decorative)
- The "unforgettable element" (Garden in Bloom)
- Bold aesthetic direction (interpreted as refined minimalism)

### Eden Philosophy

- Associates are Primary Clients
- Friction Feed: Show exceptions, not dashboards
- Silent Admin: Monitor reality, don't become primary data store
- Support Insights, not KPIs

---

*Design System v2.0 — January 2026*
*With Frontend-Design Skill integration*
