# EDEN HUB — FOUNDATION DOCUMENT

**Version:** 2.0
**Date:** 18 January 2026
**Purpose:** Master specification for Eden Hub Portal
**Status:** Prototype Complete - Ready for Integration

---

## 1. WHAT IS EDEN HUB?

Eden Hub is the Associates Portal for Eden Relationships Ltd — a therapy practice that treats its seven associates (targeting sixteen) as "Primary Clients" rather than employees.

**The Core Philosophy:** Eden is a steward, not a manager. The portal serves associates; it doesn't monitor them.

---

## 2. CURRENT IMPLEMENTATION STATUS

### 2.1 Completed Features (v0.6.0)

| Module | Status | Description |
|--------|--------|-------------|
| **Core Design System** | Complete | Eden Calm CSS variables, no grey palette |
| **Associates** | Complete | ID cards, 7-tab detail panels, capacity tracking |
| **Clients** | Complete | Cards, 7-stage pipeline, detail panels |
| **Schedule** | Complete | Monthly calendar, session management |
| **Action Centre** | Complete | Friction Feed, summary grid, resolution drawer |
| **Financial Hub** | Complete | True Cash, Cash Density, Tax Intelligence, Payout Cockpit, Wealth Lab |
| **Referrals** | Complete | Admin workflow, associate interest, specialisation matching |
| **Contracts** | Complete | Document grid, status tracking |
| **Messages** | Complete | Inbox, message viewer, compose |
| **Support** | Complete | Help links, emergency contacts |
| **CPD** | Placeholder | Activities list structure |

### 2.2 Technical Approach

- **Single-file HTML prototype** (~900KB)
- **Mock data** for all entities (7 associates, 20+ clients, 4 referrals)
- **Vanilla JavaScript** (no framework dependencies)
- **Responsive design** (768px breakpoint)

### 2.3 Next Phase

- Airtable live data integration
- Make.com automation connections
- Squarespace authentication
- Mobile testing and refinement
- React migration (when appropriate)

---

## 3. DESIGN PHILOSOPHY

### 3.1 Stewardship Principles

| Principle | What It Means | How It's Implemented |
|-----------|---------------|----------------------|
| **Associates = Primary Clients** | The portal exists to support them, not track them | No management dashboards, no productivity metrics |
| **Passive Monitoring** | Portal quietly tracks data in background | Only surfaces exceptions that need attention |
| **Friction Feed** | Action Centre shows ONLY exceptions | No dashboard noise, no vanity metrics |
| **Soft Enforcement** | Warnings, not blocks | Credits flag as "overdue" but don't prevent work |
| **Silent Admin** | Goal is invisible administration | Associates focus on clients, not paperwork |

### 3.2 The "Maps-Style" Navigation Pattern

The portal follows the Google Maps interaction paradigm:

**Surface View → Drill-Down → Detail**

When you tap a card:
- **On Desktop:** A Side Panel slides in from the right (450px width)
- **On Mobile:** A Bottom Sheet slides up from the bottom (85% screen height)

This prevents users getting "lost" in nested screens while maintaining context.

**Transitions:** Fade & Slide (300ms ease-out)

---

## 4. EDEN CALM DESIGN SYSTEM

### 4.1 Colour Palette

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

### 4.2 Alert Colours (Friction Feed Only)

| Colour | Hex | When Used |
|--------|-----|-----------|
| Amber | `#F59E0B` | Pending items, soft warnings |
| Rose | `#EF4444` | Urgent items, overdue actions |
| Blue | `#3B82F6` | Informational |

### 4.3 Logo

**Simple Outlined Leaf** — single elegant leaf with stem, 1.5px stroke, no fill.

**DO NOT USE:** The "ER" monogram from earlier iterations.

### 4.4 Typography

- **Font Family:** System fonts (`-apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif`)
- **Base Size:** 16px
- **Line Height:** 1.6
- **Icons:** 1.5px thin-stroke outlined style throughout (Lucide)

### 4.5 Component Styling

- **Border Radius:** 8px standard, 12px for cards
- **Shadows:** Subtle, used sparingly
- **Animations:** Fade & Slide (300ms ease-out)

---

## 5. DATA ARCHITECTURE

### 5.1 UCID System

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
| `REF` | `REF-25003` | Referral |
| `CON` | `CON-001` | Contract |

**UCID is the primary key** across all Airtable tables.

### 5.2 Key Formulas

**True Cash** (lead metric for Financial Vitality Hub):
```
Bank Balance - Unspent Credits - Associate Payouts Owed - 25% Tax Reserve
```

**Capacity %** (for associates):
```
(Active Clients / Max Capacity) × 100
```

**Revenue Split:**
```
Associate: 69%
Eden: 31%
```

### 5.3 Support Modes

Associates operate in one of two modes:

| Mode | Badge | Meaning |
|------|-------|---------|
| **Independent** | `✓ Independent` | Self-managing, minimal oversight |
| **Supported** | `◐ Supported` | Receiving additional guidance/mentoring |

---

## 6. PORTAL STRUCTURE

### 6.1 Navigation Modules (Admin View)

| Module | Purpose | View Type |
|--------|---------|-----------|
| **Action Centre** | Friction Feed — exceptions only | Summary + List |
| **Associates** | ID cards for all associates | Grid |
| **Clients** | ID cards for all clients | Grid |
| **Schedule** | Session calendar | Calendar |
| **Finance** | Financial Vitality Hub | Gateway cards |
| **Referrals** | Client allocation workflow | Stats + List |
| **Contracts** | Document tracking | Grid |
| **Messages** | Communications | List |
| **Support** | Help resources | Links |
| **CPD** | Professional development | List |

### 6.2 Detail Panel Architecture

**Associate Detail Panel (7 Tabs)**
1. Overview - Quick stats, client count, earnings
2. Contact - Email, phone, address, emergency
3. Sessions - Upcoming and past (timeline)
4. Contracts - Agreement status
5. Finance - Earnings, invoices, payout history
6. Inbox - Direct messages
7. Clients - Pipeline strip + client list

**Client Detail Panel (5 Tabs + Pipeline)**
1. Contact - Email, phone, referral source
2. Sessions - History and upcoming
3. Finance - Payments, credits
4. Notes - Internal notes
5. Timeline - Activity log
+ Pipeline tracker at top (7-stage journey)

### 6.3 Adaptive Layout Behaviour

| Breakpoint | Layout |
|------------|--------|
| **> 768px (Desktop)** | Sidebar visible, Side Panel for details (slides from right) |
| **≤ 768px (Mobile)** | Sidebar hidden, Bottom Sheet for details (slides from bottom) |

---

## 7. CLIENT JOURNEY PIPELINE (7 Stages)

```
INQUIRY → ENGAGED → MATCHED → BOOKED → ACTIVE → FOLLOW-UP → ONGOING
 Amber    Purple     Blue      Teal     Green     Coral       Gold
```

| Stage | Meaning | Colour |
|-------|---------|--------|
| **Inquiry** | Lead received, not yet responded | #F59E0B |
| **Engaged** | Eden has responded, building trust | #8B5CF6 |
| **Matched** | Suitable associate assigned | #3B82F6 |
| **Booked** | Session scheduled, payment received | #14B8A6 |
| **Active** | Ongoing therapeutic relationship | #10B981 |
| **Follow-Up** | Post-session check-in | #F97316 |
| **Ongoing** | Retained client, referral source | #EAB308 |

---

## 8. REFERRAL SYSTEM

### 8.1 Referral Workflow

```
NEW → TRIAGE → BROADCAST → PENDING → ALLOCATED → ACCEPTED
```

1. **New** - Inquiry received via website form
2. **Triage** - Admin reviews, assigns pseudonym, selects specialisations
3. **Broadcast** - Sent to matching associates (24hr window)
4. **Pending** - Associates have expressed interest, awaiting allocation
5. **Allocated** - Admin selects associate
6. **Accepted** - Associate confirms, client becomes their responsibility

### 8.2 Specialisations (24 Categories)

Anxiety & Stress, Depression, Trauma & PTSD, Grief & Loss, Relationships & Intimacy, Couples & Marriage, Pre-Marital Preparation, Family Dynamics, Workplace & Career, Burnout & Work Stress, Leadership & Executive Performance, Identity & Self-Worth, Cultural & Minority Identity, Men's Issues, Women's Issues, Impostor Syndrome, Neurodiversity, Eating Disorders, Addictions, Loneliness & Isolation, Life Transitions, Parenting, Chronic Illness & Health, Faith & Spirituality

---

## 9. FINANCIAL VITALITY HUB

### 9.1 Wealth Hub Modules

| Module | Purpose | Status |
|--------|---------|--------|
| **Cash Density** | 3-month cash flow projection | Complete |
| **Tax Intelligence** | VAT tracking (pre-threshold mode) | Complete |
| **Payout Cockpit** | Associate payment management | Complete |
| **Wealth Lab Simulator** | Dividend vs pension planning | Complete |
| **System Health** | Integration status | Placeholder |

### 9.2 True Cash Pulse Indicator

| Status | Colour | Meaning |
|--------|--------|---------|
| Healthy | Green | >3 months runway |
| Caution | Amber | 1-3 months runway |
| Critical | Red | <1 month runway |

---

## 10. TECHNICAL STACK

### 10.1 Current (Prototype)

| Layer | Technology |
|-------|------------|
| **Frontend** | Single-file HTML + CSS + JavaScript |
| **Styling** | CSS Custom Properties |
| **Icons** | Lucide (inline SVG, 1.5px stroke) |
| **Data** | Mock JavaScript arrays |

### 10.2 Target (Production)

| Layer | Technology |
|-------|------------|
| **Frontend** | React 18 + TypeScript |
| **Styling** | Tailwind CSS |
| **Components** | shadcn/ui |
| **Icons** | Lucide React |
| **Backend** | Airtable (database) |
| **Automation** | Make.com (workflows) |
| **Payments** | Stripe |
| **Accounting** | QuickBooks |
| **Auth** | Squarespace Member Areas |

---

## 11. SESSION PROTOCOL

### Start of Every Session

1. Read `EDEN_STATUS.txt` for current state
2. Confirm which features/chunks to work on
3. Review any new requirements

### End of Every Session

1. Update `EDEN_STATUS.txt` with progress
2. Commit changes to git
3. Note any blockers or decisions made

---

## 12. GLOSSARY

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

## 13. CONTACT & OWNERSHIP

**Eden Relationships Ltd**
- **Co-Founders:** Mike & Maryanne
- **Website:** edenrelationships.co.uk
- **Focus:** Therapy practice advocating for Black therapists

---

*This document is the single source of truth for Eden Hub development. Update it as decisions are made.*
