# AGENTS.MD - Claude's Long-Term Memory

**Purpose:** Persistent rules and context for autonomous Phase 4 implementation.
**Last Updated:** 2026-01-10

---

## Core Design Rules: Eden Calm

### Colour Palette (NO GREY ALLOWED)

| Token | Hex | Usage |
|-------|-----|-------|
| Pure White | `#FFFFFF` | Page backgrounds |
| Eden Mint | `#F4F7F6` | Card surfaces, sidebar |
| Eden Green | `#2D5F4D` | Primary actions, accents |
| Eden Border | `#D4E5DE` | Borders (green-tinted) |

**CRITICAL:** Never use grey (`#808080`, `#666`, `#ccc`, etc.). Use Eden Mint or Eden Border for subtle backgrounds.

### Icon Style

- **Library:** Lucide icons only
- **Stroke Width:** 1.5px (thin-stroke)
- **Style:** Outlined, never filled
- **Size:** 20px standard, 24px for primary actions

```html
<svg class="icon" stroke-width="1.5">...</svg>
```

### Typography

- System fonts: `-apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif`
- No custom fonts
- Base size: 16px
- Line height: 1.6

---

## Business Context

### Associates are "Primary Clients"

Eden Relationships treats its associates (therapists) as clients, not employees. This means:

- **Stewardship, not surveillance** - The portal supports, doesn't monitor
- **Passive monitoring** - System watches data silently, no manual updates required
- **Soft enforcement** - Gentle warnings, not hard blocks
- **Friction Feed** - Only shows exceptions, not dashboard noise

### Key Terminology

| Term | Meaning |
|------|---------|
| Associate | A therapist working with Eden (Primary Client) |
| Client | End-user receiving therapy |
| UCID | Unique Client ID (format: TYPE-YYSEQ) |
| Friction Feed | Exception-only display in Action Centre |
| True Cash | Available funds minus obligations and tax reserve |

---

## Implementation Patterns

### Panel Architecture

| Screen | Pattern |
|--------|---------|
| Desktop (>768px) | Side Panel slides from right (450px) |
| Mobile (<=768px) | Bottom Sheet slides from bottom (85vh) |

### Navigation Roles

| Role | Visible Modules |
|------|-----------------|
| Admin | All modules (9 items) |
| Associate | Dashboard, My Clients, My Schedule, My Earnings, CPD, Support (6 items) |

### State Variables

```javascript
let currentUserRole = 'admin'; // or 'associate'
let currentUserId = null;      // ASSOC-YYSEQ for associates
let isLoggedIn = false;
```

---

## Session Tracking

### Completed Stories
- None yet

### Current Story
- Story #1: Role-Based Navigation

### Blocked Items
- None

---

## File Backup Protocol

Before major changes:
1. Note current state in EDEN_STATUS.txt
2. Implement changes incrementally
3. Test each feature before moving on
4. Update prd.json status after completion

---

*This file is Claude's persistent memory for the Ralph loop. Update after each story completion.*
