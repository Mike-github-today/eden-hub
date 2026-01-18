# Eden Hub Portal

**Admin dashboard for Eden Relationships Ltd**

A single-file HTML prototype supporting associates (therapists) with practice management, client tracking, and financial tools.

---

## Current Status

**Version:** 0.6.0
**Last Updated:** January 2026
**Prototype Size:** ~900KB single HTML file

### Implemented Features

- **Associates Module** - ID cards, 7-tab detail panels, capacity tracking
- **Clients Module** - 7-stage pipeline tracker, detail panels
- **Schedule/Calendar** - Monthly view, session management
- **Action Centre** - Friction Feed (exception-only alerts)
- **Financial Vitality Hub** - True Cash, Cash Density, Tax Intelligence, Payout Cockpit, Wealth Lab
- **Referrals** - Admin workflow, associate interest expression, specialisation matching
- **Contracts** - Document tracking with status
- **Messages/Inbox** - Communication system
- **Support & CPD** - Help resources and professional development

### Architecture

- Single-file HTML prototype (no build tooling)
- CSS custom properties (Eden Calm design system)
- Vanilla JavaScript
- Mock data for all entities
- Responsive design (desktop side panels, mobile bottom sheets)

---

## Quick Start

1. Open `index.html` in a browser
2. Use the role toggle button (bottom-right) to switch between Admin and Associate views
3. Click on cards to open detail panels
4. Navigate using the sidebar

---

## Key Concepts

- **Associates as Primary Clients** - We serve therapists, not manage them
- **Friction Feed** - Only exceptions need attention
- **Swiss Clinic Aesthetic** - Calm, professional, no dashboard theatre
- **Silent Admin** - Automation handles the boring stuff

---

## Documentation

| Document | Purpose |
|----------|---------|
| `EDEN_MASTER.md` | Complete technical specification |
| `PROJECT_CONTEXT.md` | Philosophy and goals |
| `CLAUDE.md` | AI development instructions |
| `CONTRIBUTING.md` | Technical conventions |
| `CHANGELOG.md` | Version history |
| `EDEN_STATUS.txt` | Session handoff |
| `agents.md` | Claude's persistent memory |
| `EDEN_HUB_FOUNDATION.md` | Original foundation document |

---

## Folder Structure

```
├── index.html              ← Main prototype (all code)
├── docs/decisions/         ← Architecture Decision Records
├── docs/strategy/          ← Business planning documents
├── docs/specs/             ← Component specifications
├── phases/                 ← Development phases
├── exports/                ← Claude session outputs
└── _archive/               ← Old versions
```

---

## Tech Stack

| Layer | Technology |
|-------|------------|
| Frontend | Single-file HTML + CSS + JavaScript |
| Future Framework | React 18 + TypeScript |
| Styling | CSS Custom Properties (Tailwind ready) |
| Components | shadcn/ui (future) |
| Database | Airtable (planned integration) |
| Automation | Make.com (planned integration) |
| Hosting | Vercel (planned) |
| Auth | Squarespace Member Areas (planned) |

---

## Design System: Eden Calm

### Colours

```css
--pure-white: #FFFFFF;      /* Page backgrounds */
--eden-mint: #F4F7F6;       /* Card surfaces */
--eden-green: #2D5F4D;      /* Primary actions */
--eden-border: #D4E5DE;     /* Borders (no grey!) */
```

### Principles

- No grey palette (Eden Mint for subtle backgrounds)
- Thin-stroke Lucide icons (1.5px)
- System fonts only
- Soft enforcement (warnings, not blocks)

---

## Next Steps

1. Airtable live data integration
2. Make.com webhook connections
3. Squarespace authentication
4. Mobile testing and refinement
5. React migration when appropriate

---

## Contact

Eden Relationships Ltd
Technical Lead: Mike

---

*Built with care for associates who deserve better tools*
