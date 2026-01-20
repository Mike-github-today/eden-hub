# CLAUDE.md

**Purpose:** Auto-read instructions for Claude Code sessions working on Eden Hub Portal.

---

## ⚠️ IMPLEMENTATION MODE - READ FIRST

When Mike gives you chunks or tasks to implement, follow this workflow **exactly**:

### Default Behaviour

1. **Work sequentially** through all chunks/tasks given
2. **Create backup before each change** (portal_v1 → v2 → v3)
3. **Follow the spec exactly** - no improvisation unless spec is unclear
4. **Confirm briefly** what was done after each chunk (2-3 sentences max)
5. **Proceed immediately** to the next chunk - don't wait for permission

### Git Workflow

- **Push directly to main branch** - no feature branches for this project
- After implementing chunks, commit and push to main
- Commit message format: `feat: Chunk X - [brief description]`

### Only Stop and Ask If

- You encounter an error you cannot resolve
- Something in the spec is unclear or contradictory
- A design decision genuinely needs Mike's input
- You've completed ALL chunks in the batch

### Do NOT Stop To

- Ask "shall I continue?" - yes, always continue
- Explain what you're about to do - just do it
- Request confirmation between chunks - keep going
- Summarise at length - brief confirmations only

### Example Flow

```
Mike: "Work through chunks 1-4"

Claude: [implements chunk 1, backs up files]
"✓ Chunk 1 complete: Foundation setup with design tokens."
[immediately implements chunk 2]
"✓ Chunk 2 complete: Header with Eden logo and navigation."
[immediately implements chunk 3]
"✓ Chunk 3 complete: Sidebar with gateway icons."
[immediately implements chunk 4]
"✓ Chunk 4 complete: Gateway cards grid on Command Centre."

"All 4 chunks complete. Ready for chunks 5-7 when you are."
```

---

## Project Overview

Eden Hub Portal is a React-based admin dashboard for Eden Relationships Ltd, a therapy practice. The portal serves **associates (therapists)** as Primary Clients, not employees.

**Key Philosophy:** "Stewardship" - supporting independent practitioners through silent automation and soft enforcement, never surveillance or hard blocks.

---

## Critical Context Files

Always read these before starting work:

| File | Purpose |
|------|---------|
| `EDEN_MASTER.md` | Complete specification (design tokens, pipelines, architecture) |
| `EDEN_STATUS.txt` | Session handoff - what was last worked on |
| `docs/decisions/ADR-*.md` | Architecture decisions (auth, etc.) |

---

## Design System Quick Reference

### Colours

```css
--eden-deep: #2d5f4d;      /* Primary green - buttons, CTAs */
--eden-whisper: #f4f7f6;   /* Card backgrounds (Eden Mint) */
--eden-white: #ffffff;     /* Page backgrounds */
--eden-text: #1a1a1a;      /* Primary text */
```

### Pipeline Stage Colours

```css
--stage-inquiry: #f59e0b;   /* Amber */
--stage-engaged: #8b5cf6;   /* Purple */
--stage-matched: #3b82f6;   /* Blue */
--stage-booked: #14b8a6;    /* Teal */
--stage-active: #10b981;    /* Green */
--stage-followup: #f97316;  /* Coral */
--stage-ongoing: #eab308;   /* Gold */
```

### Icons

**Lucide React only.** Thin-stroke outlined icons (1.5px weight). Never filled icons.

```jsx
import { Users, Calendar, Wallet } from 'lucide-react';

// Correct usage
<Users className="w-5 h-5" strokeWidth={1.5} />
```

---

## UCID Format

**Pattern:** `TYPE-YYSEQ`

- Associates: `ASC-2401`
- Clients: `CLI-2507`
- Sessions: `SES-2501`

Always use monospace font for UCIDs.

---

## Panel Patterns

| Screen | Pattern |
|--------|---------|
| Desktop | Side Panel (from right) |
| Mobile | Bottom Sheet (from bottom) |

---

## Current Implementation Status

Check `EDEN_STATUS.txt` for:
- Last completed work
- Current chunk/phase
- Next priorities
- Known issues

---

## Development Rules

1. **Backup before editing:** Always create `portal_v1 → portal_v2` before changes
2. **Test independently:** Each chunk should work standalone
3. **Use CSS variables:** Never hardcode colours
4. **Semantic HTML:** Proper elements, not just divs
5. **Minimal JavaScript:** Progressive enhancement preferred
6. **44px touch targets:** Mobile minimum
7. **Alt text required:** All images

---

## Tech Stack

| Layer | Technology |
|-------|------------|
| Framework | React 18 + TypeScript |
| Styling | Tailwind CSS |
| Components | shadcn/ui |
| Icons | Lucide React |
| Database | Airtable |
| Automation | Make.com |
| Hosting | Vercel |

---

## Common Tasks

### Adding a new component

1. Check EDEN_MASTER.md for design tokens
2. Use existing patterns from shadcn/ui
3. Apply Eden colour variables
4. Test responsive behaviour (desktop panel vs mobile sheet)

### Working with pipelines

- Client pipeline: 7 stages (Inquiry → Ongoing)
- Onboarding pipeline: 6 stages (Welcome → Active)
- Use stage colours from design tokens
- Show as horizontal tracker with coloured dots

### Implementing Friction Feed items

- Only show exceptions (not normal status)
- Use alert colours: Rose (urgent), Amber (warning), Blue (info)
- Include resolve action for each item
- Update count in Actions gateway

---

## Session Protocol

**At START of session:**
1. Read EDEN_STATUS.txt
2. Confirm current phase/chunk
3. Ask for any uploaded files
4. Query Airtable MCP if needed

**At END of session:**
1. Update EDEN_STATUS.txt with progress
2. Note any blockers or decisions made
3. Prompt Mike to download to OneDrive

---

## Questions to Ask Mike

If unclear about:
- Business logic → Ask before implementing
- Design decisions → Check EDEN_MASTER.md first
- Technical approach → Propose options, let Mike choose

---

## Design System: Frontend-Design Skill Integration

Eden Portal follows the **Frontend-Design Skill** principles adapted for our "Eden Calm" aesthetic.

### Typography (MANDATORY)

| Role | Font | Fallback | Usage |
|------|------|----------|-------|
| **Display** | Fraunces | Georgia, serif | Headings, titles, "Garden in Bloom" states |
| **Body** | DM Sans | system-ui, sans-serif | All body text, labels, buttons |

**NEVER use these fonts:**
- Inter, Roboto, Arial, system-ui as primary
- Any generic sans-serif without explicit approval

**Why Fraunces + DM Sans?**
- Fraunces has "soft serifs" that feel therapeutic and approachable
- DM Sans is highly readable with more character than Inter
- Together they create "premium wellness" not "corporate dashboard"

### Google Fonts Import

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=DM+Sans:ital,opsz,wght@0,9..40,300;0,9..40,400;0,9..40,500;1,9..40,400&family=Fraunces:ital,opsz,wght@0,9..144,300;0,9..144,400;0,9..144,500;1,9..144,300&display=swap" rel="stylesheet">
```

### CSS Variables for Typography

```css
:root {
    --font-display: 'Fraunces', Georgia, serif;
    --font-body: 'DM Sans', system-ui, sans-serif;
}
```

### Animation Standards

Eden uses **intentional motion** — meaningful animations at key moments, not scattered micro-interactions.

| Animation | When to Use | Timing |
|-----------|-------------|--------|
| **Staggered reveal** | Cards loading in Friction Feed | 100ms delay between cards |
| **Pulse indicator** | Live status dots | 2s ease-in-out infinite |
| **Slide in** | Side Panel (desktop) | 300ms ease-out |
| **Slide up** | Bottom Sheet (mobile) | 300ms ease-out |
| **Draw-in** | "Garden in Bloom" leaf SVG | 1.5s ease-out |

**Animation Timing Variables:**

```css
:root {
    --ease-out-soft: cubic-bezier(0.23, 1, 0.32, 1);
    --duration-fast: 150ms;
    --duration-normal: 300ms;
    --duration-slow: 500ms;
}
```

### The "Unforgettable Element"

Every interface should have ONE memorable thing. For Eden Portal, this is:

1. **The calm, un-dashboard-like feel** — Friction Feed shows only exceptions
2. **Botanical warmth** — "Garden in Bloom" all-clear state with animated leaf
3. **Absence of noise** — What's NOT there is as important as what IS

### Frontend-Design Skill Reference

When building new components, Claude Code should mentally reference these principles:

- **Purpose:** What problem does this solve? Who uses it?
- **Tone:** Eden = "refined minimalism with botanical warmth"
- **Differentiation:** Does this feel like a therapy practice, not a SaaS dashboard?

Full skill documentation: `/mnt/skills/public/frontend-design/SKILL.md`

---

*Last updated: January 2026*
