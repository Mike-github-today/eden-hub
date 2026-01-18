# AGENTS.MD - Claude's Long-Term Memory

**Purpose:** Persistent rules and context for Eden Hub development sessions.
**Last Updated:** 2026-01-18

---

## Core Design Rules: Eden Calm

### Colour Palette (NO GREY ALLOWED)

| Token | Hex | Usage |
|-------|-----|-------|
| Pure White | `#FFFFFF` | Page backgrounds |
| Eden Mint | `#F4F7F6` | Card surfaces, sidebar |
| Eden Green | `#2D5F4D` | Primary actions, accents |
| Eden Green Hover | `#245040` | Hover states |
| Eden Green Light | `#E8F0ED` | Light tints, badges |
| Eden Text | `#1A3329` | Primary text |
| Eden Text Secondary | `#4A6259` | Secondary text |
| Eden Border | `#D4E5DE` | Borders (green-tinted, NOT grey) |

**CRITICAL:** Never use grey (`#808080`, `#666`, `#ccc`, etc.). Use Eden Mint or Eden Border for subtle backgrounds.

### Alert Colours (Friction Feed Only)

| Colour | Hex | When Used |
|--------|-----|-----------|
| Amber | `#F59E0B` | Pending items, soft warnings |
| Rose | `#EF4444` | Urgent items, overdue actions |
| Blue | `#3B82F6` | Informational |

### Referral System Colours

| Status | Hex | Meaning |
|--------|-----|---------|
| New | `#9B59B6` | Untriaged referral |
| Broadcasting | `#3498DB` | Sent to associates |
| Pending | `#F39C12` | Awaiting allocation |
| Accepted | `#27AE60` | Associate assigned |
| Declined | `#95A5A6` | No match found |

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
- Monospace for UCIDs: `monospace`

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
| 69/31 Split | Revenue split (69% associate, 31% Eden) |

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
| Admin | All modules (Associates, Clients, Schedule, Actions, Finance, Referrals, Contracts, Support, CPD) |
| Associate | Dashboard, My Clients, My Schedule, My Earnings, CPD, Support |

### State Variables

```javascript
let currentUserRole = 'admin'; // or 'associate'
let currentUserId = null;      // ASSOC-YYSEQ for associates
let isLoggedIn = false;
```

### Menu Configuration Pattern

Menus are role-aware and appear ONLY in detail view headers:

```javascript
const menuConfigs = {
    associate: {
        admin: ['View Profile', 'View Earnings', 'Send Message', 'View Contract'],
        associate: []  // Associates don't see menus on other associates
    },
    client: {
        admin: ['View Details', 'View Sessions', 'Message Therapist', 'Update Stage', 'divider', 'Reassign Associate'],
        associate: ['View Details', 'View Sessions', 'Send Message', 'Update Stage']
    },
    // ... etc
};
```

---

## Completed Features

### Core System
- [x] Eden Calm design system (CSS variables)
- [x] Responsive layout (sidebar, side panel, bottom sheet)
- [x] Role-based navigation (Admin vs Associate)
- [x] Role toggle for testing

### Modules
- [x] Associates (ID cards, 7-tab detail panel)
- [x] Clients (cards, 7-stage pipeline, detail panel)
- [x] Schedule/Calendar (monthly view, session detail)
- [x] Action Centre (Friction Feed, summary grid)
- [x] Financial Vitality Hub (Wealth Lab)
- [x] Referrals (admin workflow, associate interest)
- [x] Contracts (grid, detail panel)
- [x] Messages/Inbox (list, viewer, compose)
- [x] Support (links, emergency contacts)
- [x] CPD (activities placeholder)

### UX Enhancements
- [x] Empty states ("Garden in Bloom")
- [x] Unified detail view pattern
- [x] Menu standardisation (detail views only)
- [x] Progress stepper component
- [x] Toast notifications

---

## Current Session Tracking

### Last Completed Work
- Chunk 6: Three-Dots Menu Standardisation (2026-01-18)

### Next Priorities
1. Airtable data integration
2. Make.com webhook setup
3. Squarespace authentication
4. Mobile testing and refinement

### Blocked Items
- None

---

## File Backup Protocol

Before major changes:
1. Note current state in EDEN_STATUS.txt
2. Implement changes incrementally
3. Test each feature before moving on
4. Commit to git with descriptive message

---

*This file is Claude's persistent memory for Eden Hub development. Update after each session.*
