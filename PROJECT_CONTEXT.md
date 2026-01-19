# PROJECT CONTEXT

**Eden Hub Portal - The Human Story**

---

## What is Eden?

Eden Relationships Ltd is a therapy practice founded on a radical idea: **treat your practitioners like clients, not employees.**

Most therapy practices hire therapists as staff, set quotas, and measure performance with KPIs. Eden does the opposite. Associates are independent professionals who choose to work with Eden because Eden makes their lives easier, not harder.

---

## The Stewardship Philosophy

Eden operates as a **steward** of its associates' practices:

- We handle the boring stuff (admin, scheduling, payments, compliance)
- Associates focus on what they do best (therapy)
- We never surveil, judge, or pressure
- We celebrate their success without taking credit

This philosophy shapes every pixel of the portal.

---

## Why Build a Portal?

Currently, Mike and Maryanne manage everything manually:

- Tracking client inquiries in spreadsheets
- Chasing associates for insurance renewals
- Calculating revenue splits by hand
- Sending individual reminder emails

The portal automates the invisible work so Eden can scale from 7 to 16+ associates without burning out.

---

## Design Philosophy: "Swiss Clinic"

Most admin dashboards look like mission control - glowing charts, red alerts, heat maps. They're designed to make managers feel powerful.

Eden's portal is designed to feel **calm**:

- White backgrounds, soft mint cards
- No flashing, no urgency theatre
- Information appears when you need it, hides when you don't
- "All Clear!" is the goal, not endless notification badges

We call this the "Swiss Clinic" aesthetic - professional, clean, trustworthy.

---

## The Friction Feed Concept

Traditional dashboards show everything: good, bad, neutral. You have to hunt for problems.

Eden's **Friction Feed** shows only exceptions - things that need attention:

- A document is expiring in 30 days
- A client inquiry hasn't been answered in 24 hours
- An invoice is overdue

When everything is fine, you see: **"All Clear!"**

This respects the associate's time and attention. We're not here to make them feel busy.

---

## Key Concepts

### Primary Clients

Associates are Eden's primary clients. End clients (the people receiving therapy) matter deeply, but associates come first in our operational design.

### Silent Admin

The best admin is invisible. Automated reminders, auto-calculated splits, seamless payments - associates shouldn't notice the machinery.

### Soft Enforcement

When something needs attention, we nudge, not block:

- Amber dot, not red banner
- "Hey, this is expiring soon" not "ACCESS DENIED"
- Assume good intent, provide information, let them act

### Support Insights, Not KPIs

Data in the portal helps associates understand their practice:

- "You've completed 12 sessions this month"
- Not "You're 3 sessions behind target"

---

## The Team

**Mike** - Technical Lead, Co-Founder
- Day job alongside Eden work
- Builds systems and architecture
- This portal is his project

**Maryanne** - Business Lead, Co-Founder
- Leads client work and associate relationships
- Provides business requirements
- Tests and validates features

---

## Current State (January 2026)

### Business Status
- 7 active associates
- Growth target: 16 associates
- Revenue managed under VAT threshold (£85k)

### Portal Implementation Status

**Completed Features:**
- Full Eden Calm design system (CSS variables, no grey palette)
- Associates module with 7-tab detail panels
- Clients module with 7-stage pipeline tracker
- Action Centre with Friction Feed and summary grid
- Financial Vitality Hub (Wealth Lab) with:
  - True Cash calculation
  - Cash Density projections
  - Tax Intelligence (Pre-VAT mode)
  - Payout Cockpit
  - Wealth Lab Simulator
- Schedule/Calendar module
- Referral system with admin workflow and associate interest expression
- Contracts module
- Messages/Inbox system
- Support and CPD modules
- Clinical Governance module ("Silent Auditor") with:
  - Supervision Tracker (Current/Due Soon/Overdue status)
  - DBS Update Service tracking (annual or 3-year cycle)
  - ICO Registration tracking with onboarding gate
  - Compliance cards in Associate Profile
  - Friction Feed integration for compliance items
- Role-based access (Admin vs Associate views)
- Responsive design (desktop side panels, mobile bottom sheets)
- Empty states with "Garden in Bloom" illustrations

**Current Approach:**
- Single-file HTML prototype (~960KB)
- Mock data for all entities (7 associates, 20+ clients, 4 referrals, 10 friction items)
- Vanilla JavaScript (no framework dependencies)
- Ready for React migration when appropriate

**Next Phase:**
- Airtable live data integration (including clinical governance fields)
- Make.com automation connections for compliance tracking
- Squarespace authentication
- Mobile testing and refinement

---

## Success Looks Like

A year from now:

- Associates log in, see "All Clear!" or handle 2-3 friction items
- Mike and Maryanne spend 80% less time on admin
- Onboarding a new associate takes hours, not days
- Associates recommend Eden to colleagues

---

## Principles for Development

1. **Would an associate thank us for this?** If not, reconsider.
2. **Does this reduce friction?** If it adds steps, justify them.
3. **Is this visible only when needed?** Default to hidden.
4. **Can it break silently?** Build with automation, but monitor.
5. **Does it feel calm?** No urgency theatre.

---

*This document explains WHY we're building what we're building. For HOW, see EDEN_MASTER.md.*
