# EDEN HUB — FOUNDATION DOCUMENT

**Version:** 1.0  
**Date:** 6 January 2026  
**Purpose:** Master specification for fresh Eden Hub repository  
**Context:** Replacing previous "eden-admin-portal" iterations

---

## 1. WHAT IS EDEN HUB?

Eden Hub is the Associates Portal for Eden Relationships Ltd — a therapy practice that treats its seven associates (targeting sixteen) as "Primary Clients" rather than employees.

**The Core Philosophy:** Eden is a steward, not a manager. The portal serves associates; it doesn't monitor them.

---

## 2. DESIGN PHILOSOPHY

### 2.1 Stewardship Principles

| Principle | What It Means | How It's Implemented |
|-----------|---------------|----------------------|
| **Associates = Primary Clients** | The portal exists to support them, not track them | No management dashboards, no productivity metrics |
| **Passive Monitoring** | Portal quietly tracks data in background | Only surfaces exceptions that need attention |
| **Friction Feed** | Action Centre shows ONLY exceptions | No dashboard noise, no vanity metrics |
| **Soft Enforcement** | Warnings, not blocks | Credits flag as "overdue" but don't prevent work |
| **Silent Admin** | Goal is invisible administration | Associates focus on clients, not paperwork |

### 2.2 The "Maps-Style" Navigation Pattern

The portal follows the Google Maps interaction paradigm:

**Surface View → Drill-Down → Detail**

When you tap a card:
- **On iPhone:** A Bottom Sheet slides up from the bottom (85% screen height)
- **On Laptop:** A Side Panel slides in from the right (450px width)

This prevents users getting "lost" in nested screens while maintaining context.

**Transitions:** Fade & Slide (300ms ease-out)

---

## 3. EDEN CALM DESIGN SYSTEM

### 3.1 Colour Palette

The palette deliberately **avoids grey** to maintain warmth and approachability.

| Token | Hex | Usage |
|-------|-----|-------|
| Pure White | `#FFFFFF` | Page backgrounds |
| Eden Mint | `#F4F7F6` | Card surfaces, sidebar |
| Eden Green | `#2D5F4D` | Primary actions, accents, headers |
| Eden Green Hover | `#245040` | Hover states |
| Eden Green Light | `#E8F0ED` | Light tints, badges |
| Eden Text | `#1A3329` | Primary text |
| Eden Text Secondary | `#4A6259` | Secondary text |
| Eden Border | `#D4E5DE` | Borders (green-tinted, NOT grey) |

### 3.2 Alert Colours (Friction Feed Only)

| Colour | Hex | When Used |
|--------|-----|-----------|
| Amber | `#F59E0B` | Pending items, soft warnings |
| Rose/Red | `#EF4444` | Urgent items, overdue actions |
| Blue | `#3B82F6` | Informational |

### 3.3 Logo

**Simple Outlined Leaf** — single elegant leaf with stem, 1.5px stroke, no fill.

```svg
<svg viewBox="0 0 32 32" fill="none" stroke="currentColor" stroke-width="1.5">
  <path d="M16 28 L16 12" stroke-linecap="round"/>
  <path d="M16 12 C16 12, 8 14, 6 20 C4 26, 10 28, 16 24 C22 28, 28 26, 26 20 C24 14, 16 12, 16 12" stroke-linejoin="round"/>
  <path d="M16 12 C16 16, 12 20, 10 22" stroke-linecap="round"/>
  <path d="M16 14 C17 16, 20 19, 22 20" stroke-linecap="round"/>
</svg>
```

**DO NOT USE:** The "ER" monogram from earlier iterations.

### 3.4 Typography

- **Font Family:** System fonts (`-apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif`)
- **Base Size:** 16px
- **Line Height:** 1.6
- **Icons:** 1.5px thin-stroke outlined style throughout

### 3.5 Component Styling

- **Border Radius:** 8px standard, 12px for cards
- **Shadows:** Subtle, used sparingly
- **Animations:** Fade & Slide (300ms ease-out)

---

## 4. DATA ARCHITECTURE

### 4.1 UCID System

Every entity has a **Unique Client ID** in the format:

```
TYPE-YYSEQ
```

| Type | Example | Description |
|------|---------|-------------|
| `ASSOC` | `ASSOC-2401` | Associate (2024, sequence 01) |
| `CLIENT` | `CLIENT-2501` | Client (2025, sequence 01) |
| `SESSION` | `SESSION-2501` | Session record |
| `TXN` | `TXN-2501` | Transaction |

**UCID is the primary key** across all Airtable tables.

### 4.2 Key Formulas

**True Cash** (lead metric for Financial Vitality Hub):
```
Bank Balance - Unspent Credits - Associate Payouts Owed - 25% Tax Reserve
```

**Capacity %** (for associates):
```
(Active Clients / Max Capacity) × 100
```

### 4.3 Support Modes

Associates operate in one of two modes:

| Mode | Badge | Meaning |
|------|-------|---------|
| **Independent** | `✓ Independent` | Self-managing, minimal oversight |
| **Supported** | `◐ Supported` | Receiving additional guidance/mentoring |

---

## 5. PORTAL STRUCTURE

### 5.1 Navigation Modules

| Module | Purpose | View Type |
|--------|---------|-----------|
| **Action Centre** | Friction Feed — exceptions only | List |
| **Associates** | ID cards for all associates | Grid |
| **Clients** | ID cards for all clients | Grid |
| **Earnings** | Financial Vitality Hub entry | Gateway card |
| **Schedule** | Session calendar | Calendar |
| **CPD** | Continuing Professional Development | Tracker |
| **Support** | Help and resources | Documentation |

### 5.2 ID Card Structure

Each Associate or Client ID Card opens a detail panel with **5 tabs**:

| Tab | Contents |
|-----|----------|
| **Contact** | Name, email, phone, address, emergency contact |
| **Sessions** | Session history, upcoming appointments, journey timeline |
| **Contracts** | Signed agreements, pending documents |
| **Finance** | Payment history, outstanding credits, 69/31 split breakdown |
| **Inbox** | Messages, communications history |

### 5.3 Adaptive Layout Behaviour

| Breakpoint | Layout |
|------------|--------|
| **> 768px (Desktop)** | Sidebar visible, Side Panel for details (slides from right) |
| **≤ 768px (Mobile)** | Sidebar hidden, Bottom Sheet for details (slides from bottom) |

---

## 6. FINANCIAL VITALITY HUB

The Finance section is an **intelligence layer**, not an accounting tool.

### 6.1 Finance Gateway

The "Earnings" card in the Command Centre shows:
- **True Cash** total (the lead metric)
- **VAT Progress Ring** (subtle visual)

Tapping opens the Wealth Hub.

### 6.2 Wealth Hub Modules

| Module | Purpose | Key Features |
|--------|---------|--------------|
| **Cash Density** | 3-month cash flow projection | Safe vs Growth scenario toggle, Runway indicator |
| **Tax Intelligence** | VAT tracking (pre and post threshold) | Progress ring, Days to Threshold, Reclaim tracker |
| **Payout Cockpit** | Associate payment summary | Individual cards, 69/31 split, payment status |
| **Wealth Lab Simulator** | Strategic planning tool | Dividend vs Pension sliders, ISA Bridge Gap tracker |
| **System Health** | Integration status | QuickBooks/Stripe sync monitoring |

### 6.3 Tax Intelligence Modes

**Pre-VAT (Revenue < £85k):**
- Circular progress ring (% of threshold)
- Days to Threshold estimate
- Scenario modelling (+5/+10/+15 clients)
- VAT Cliff warning at 80%+

**Post-VAT (Revenue ≥ £85k):**
- VAT Collected / Reclaimable / Net Position cards
- Quarterly Return countdown
- Reclaim Opportunities panel
- Categories: Software, Insurance, Accountancy, Training

---

## 7. FRICTION FEED SYSTEM

The Action Centre uses a "Friction Feed" — it shows **nothing** when everything is fine.

### 7.1 Friction Types

| Type | Trigger | Alert Level |
|------|---------|-------------|
| **Overdue Invoice** | 7+ days unpaid | Amber |
| **Failed Payment** | Card declined | Rose |
| **Payout Pending** | Approval required | Amber |
| **Sync Error** | QuickBooks/Stripe failed | Rose |
| **VAT Warning** | 80%+ of threshold | Amber |
| **Contract Pending** | Unsigned > 3 days | Amber |
| **Session Unconfirmed** | 24h before, no confirmation | Blue |

### 7.2 Alert Dot Behaviour

- Dots **pulse** only when active
- Dots **glow** based on urgency level
- No alerts = "All clear!" message

---

## 8. AUTHENTICATION STRATEGY

### 8.1 Overview

Authentication via **Squarespace Member Areas** integrated with **Make.com** workflows.

### 8.2 Session Flow

1. Associate logs in via Squarespace Member Areas
2. Make.com webhook captures login event
3. Session token generated and stored in Airtable
4. Portal validates token on each request
5. Token expires after inactivity (configurable)

### 8.3 Portal Entry Points

- **Primary:** Squarespace Member Areas (for associates)
- **Admin:** Direct portal access (for Mike/Maryanne)

---

## 9. TECHNICAL STACK

### 9.1 Production Stack

| Layer | Technology |
|-------|------------|
| **Frontend** | React 18 + TypeScript |
| **Styling** | Tailwind CSS |
| **Components** | shadcn/ui |
| **Icons** | Lucide (1.5px stroke weight) |
| **Backend** | Airtable (database) |
| **Automation** | Make.com (workflows) |
| **Payments** | Stripe |
| **Accounting** | QuickBooks |
| **Auth** | Squarespace Member Areas |

### 9.2 Development Approach

**Single-file HTML prototypes first** — understand and approve each component before migrating to React.

This ensures:
- Mike understands every line of code
- No "black box" components
- Clear migration path

---

## 10. IMPLEMENTATION ROADMAP

### Phase 1 (Week 1-2): Foundation
- [ ] Set up Eden Hub repository
- [ ] Create base HTML prototype with Eden Calm styling
- [ ] Implement ID Card grid (mock data)
- [ ] Implement adaptive UI (Bottom Sheet / Side Panel)
- [ ] Implement 5-tab detail panels

### Phase 2 (Week 3-4): Financial Vitality Hub
- [ ] Finance Gateway card
- [ ] Cash Density module
- [ ] Tax Intelligence (Pre-VAT mode)
- [ ] Payout Cockpit

### Phase 3 (Week 5-6): Advanced Features
- [ ] Tax Intelligence (Post-VAT mode)
- [ ] Wealth Lab Simulator
- [ ] System Health monitoring
- [ ] Friction Feed integration

### Phase 4 (Week 7-8): Integration & Polish
- [ ] Airtable connection (live data)
- [ ] Make.com webhook setup
- [ ] Squarespace authentication
- [ ] Mobile optimisation
- [ ] User testing with associates

---

## 11. FILE NAMING CONVENTIONS

| File Type | Pattern | Example |
|-----------|---------|---------|
| **Prototypes** | `eden-hub-[module]-v[n].html` | `eden-hub-dashboard-v1.html` |
| **Status Files** | `EDEN_STATUS.txt` | Always this name |
| **Specifications** | `EDEN_[NAME]_SPEC.md` | `EDEN_AUTH_SPEC.md` |
| **Handover Docs** | `EDEN_[MODULE]_HANDOVER.md` | `EDEN_FINANCE_HANDOVER.md` |

---

## 12. SESSION PROTOCOL

### Start of Every Session

1. Upload `EDEN_STATUS.txt`
2. Upload any relevant specification documents
3. State which module/phase you want to work on
4. Claude will read context before proceeding

### End of Every Session

1. Claude updates `EDEN_STATUS.txt`
2. Claude provides download link
3. Mike downloads to OneDrive before closing chat

This eliminates context drift between sessions.

---

## 13. GLOSSARY

| Term | Definition |
|------|------------|
| **True Cash** | Available funds minus obligations and tax reserve |
| **Friction Feed** | Exception-only display (nothing = all clear) |
| **UCID** | Unique Client ID format: TYPE-YYSEQ |
| **Primary Clients** | How Eden refers to associates (not employees) |
| **Silent Admin** | Goal of invisible administration |
| **Soft Enforcement** | Warnings not blocks |
| **Stewardship** | Eden's management philosophy |
| **Eden Calm** | The design aesthetic (white, mint, green — no grey) |
| **Wealth Lab** | Interactive financial planning simulator |
| **VAT Cliff** | Warning zone at 80%+ of £85k threshold |
| **69/31 Split** | Revenue split (69% to associate, 31% to Eden) |

---

## 14. CONTACT & OWNERSHIP

**Eden Relationships Ltd**
- **Co-Founders:** Mike & Maryanne
- **Website:** edenrelationships.co.uk
- **Focus:** Therapy practice advocating for Black therapists

---

*This document is the single source of truth for Eden Hub development. Update it as decisions are made.*
