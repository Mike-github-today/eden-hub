# EDEN MASTER SPECIFICATION

**Version:** 3.2
**Last Updated:** January 2026
**Status:** Prototype Complete (v0.7.0) - Ready for Integration

---

## Quick Reference

| Item | Value |
|------|-------|
| **Project** | Eden Hub Portal |
| **Current Stack** | Single-file HTML + CSS + JavaScript (~960KB) |
| **Target Stack** | React 18 + TypeScript, Tailwind CSS, shadcn/ui |
| **Database** | Airtable (planned integration) |
| **Automation** | Make.com (planned integration) |
| **Hosting** | Vercel (planned) |
| **Auth** | Squarespace Member Areas (see ADR-001) |

## Implementation Status

| Module | Status |
|--------|--------|
| Core Design System | Complete |
| Associates | Complete |
| Clients | Complete |
| Schedule/Calendar | Complete |
| Action Centre | Complete |
| Financial Hub | Complete |
| Referrals | Complete |
| Contracts | Complete |
| Messages | Complete |
| Support/CPD | Complete |
| Clinical Governance | Complete |

---

## 1. CORE PHILOSOPHY

### The Stewardship Principle

Eden treats **Associates as Primary Clients** rather than employees. Every design decision flows from this.

| Concept | Description | Implementation |
|---------|-------------|----------------|
| **Passive Monitoring** | System watches data silently | No manual status updates required |
| **Soft Enforcement** | Gentle warnings, not hard blocks | Amber indicators, not error messages |
| **Silent Admin** | Portal does heavy lifting invisibly | Automation handles routine tasks |
| **Support Insights** | Helpful data, not KPIs | Information empowers, never judges |
| **Friction Feed** | Only exceptions surface | Clean slate when everything is fine |

### Swiss Clinic Aesthetic

The portal rejects "dashboard theatre" (glowing indicators, heat maps, visual intensity) for calm, professional information design.

| Principle | Implementation |
|-----------|----------------|
| Pure White Backgrounds | Page backgrounds use #FFFFFF |
| Eden Mint Card Surfaces | Cards use #F4F7F6 |
| Eden Green Accents | #2D5F4D for action buttons and highlights |
| Thin-Stroke Icons | 1.5px outlined icons, never filled |
| No Visual Loudness | No glows, heat maps, flashing alerts |
| Subtle Triage | Tiny dots for alerts, non-glowing |
| Information on Demand | Details revealed by interaction |

---

## 2. DESIGN TOKENS

```css
:root {
  /* Primary Greens (Dark to Light) */
  --eden-forest: #1a3c34;        /* Deepest - headers, primary CTAs */
  --eden-deep: #2d5f4d;          /* Primary brand - buttons, active states */
  --eden-sage: #4a7c6f;          /* Secondary - hover states */
  --eden-muted: #6b9b8a;         /* Tertiary - icons, subtle elements */
  --eden-soft: #a8c5b8;          /* Highlights - badges, tags */
  --eden-mint: #d4e5dc;          /* Light accents - backgrounds, borders */
  --eden-pale: #e8f2ed;          /* Subtle backgrounds */
  --eden-whisper: #f4f7f6;       /* Card surfaces (Eden Mint) */
  
  /* Neutrals */
  --eden-white: #ffffff;
  --eden-text: #1a1a1a;
  --eden-text-secondary: #6b7c75;
  --eden-grey: #9ca3a0;
  --eden-grey-dark: #4a5552;
  --eden-charcoal: #2c3533;
  
  /* Pipeline Stages (7-Stage Client Journey) */
  --stage-inquiry: #f59e0b;      /* Amber */
  --stage-engaged: #8b5cf6;      /* Purple */
  --stage-matched: #3b82f6;      /* Blue */
  --stage-booked: #14b8a6;       /* Teal */
  --stage-active: #10b981;       /* Green */
  --stage-followup: #f97316;     /* Coral */
  --stage-ongoing: #eab308;      /* Gold */
  --stage-archived: #6b7280;     /* Grey */
  
  /* Onboarding Stages (6-Stage Associate Journey) */
  --onboard-welcome: #f59e0b;    /* Amber */
  --onboard-docs: #8b5cf6;       /* Purple */
  --onboard-profile: #3b82f6;    /* Blue */
  --onboard-policy: #14b8a6;     /* Teal */
  --onboard-data: #f97316;       /* Coral */
  --onboard-active: #10b981;     /* Green */
  
  /* Document Status */
  --doc-missing: #f43f5e;        /* Rose */
  --doc-pending: #f59e0b;        /* Amber */
  --doc-verified: #10b981;       /* Green */
  --doc-expiring: #f97316;       /* Orange */
  --doc-expired: #f43f5e;        /* Rose */
  
  /* Alert Colours (Triage Dots) */
  --alert-amber: #f59e0b;
  --alert-rose: #f43f5e;
  --alert-blue: #3b82f6;
  
  /* Typography */
  --font-primary: 'Inter', -apple-system, BlinkMacSystemFont, sans-serif;
  --font-mono: 'SF Mono', 'Fira Code', monospace;
  
  /* Spacing */
  --space-xs: 4px;
  --space-sm: 8px;
  --space-md: 16px;
  --space-lg: 24px;
  --space-xl: 32px;
  
  /* Radius */
  --radius-sm: 6px;
  --radius-md: 10px;
  --radius-lg: 12px;
  --radius-xl: 16px;
  
  /* Shadows */
  --shadow-subtle: 0 1px 3px rgba(26, 60, 52, 0.06);
  --shadow-soft: 0 2px 8px rgba(26, 60, 52, 0.08);
  --shadow-medium: 0 4px 16px rgba(26, 60, 52, 0.10);
  --shadow-hover: 0 6px 24px rgba(26, 60, 52, 0.12);
}
```

---

## 3. CLIENT JOURNEY PIPELINE (7 Stages)

```
INQUIRY → ENGAGED → MATCHED → BOOKED → ACTIVE → FOLLOW-UP → ONGOING
 Amber    Purple     Blue      Teal     Green     Coral       Gold
```

| Stage | Meaning | Goal | Duration | Triage Alert |
|-------|---------|------|----------|--------------|
| **Inquiry** | Lead received, not yet responded | Capture interest | 0-24 hours | >24hrs |
| **Engaged** | Eden has responded, building trust | Clarify needs | 1-7 days | >7 days inactive |
| **Matched** | Suitable associate assigned | Ensure compatibility | 1-3 days | >3 days no booking |
| **Booked** | Session scheduled, payment received | Secure commitment | Until first session | - |
| **Active** | Ongoing therapeutic relationship | Deliver value | Weeks to months | >30 days no session |
| **Follow-Up** | Post-session check-in | Strengthen relationship | 1-7 days | - |
| **Ongoing** | Retained client, referral source | Maximise lifetime value | Indefinite | >90 days dormant |

### Simplified View (4 Groups)

For compact displays:
- **New** (Amber): Inquiry + Engaged
- **Matching** (Blue): Matched + Booked
- **Active** (Green): Active
- **Nurture** (Gold): Follow-Up + Ongoing

---

## 4. ASSOCIATE ONBOARDING PIPELINE (6 Stages)

```
WELCOME → DOCS → PROFILE → POLICY → DATA → ACTIVE
 Amber   Purple   Blue      Teal    Coral   Green
```

| Stage | What Happens | Triage Alert |
|-------|--------------|--------------|
| **Welcome** | Orientation call, intro to Eden's vision | >3 days no call |
| **Documentation** | Collect & verify compliance documents | Document missing >7 days |
| **Profile Setup** | Supervisor, bank, headshot, bio, hours | Incomplete >5 days |
| **Policy Review** | Acknowledge 6 policies | Unacknowledged >7 days |
| **Data Agreement** | Sign data responsibility matrix | Unsigned >5 days |
| **Active** | Ready to receive client referrals | - |

### Required Documents (Stage 2)

| Document | Verification | Expiry |
|----------|--------------|--------|
| Associate Referral Agreement | Signature | Annual |
| Professional Indemnity Insurance | Policy number, dates | Tracked |
| Professional Membership | BACP/UKCP/NCPS/ACC number | Annual |
| Qualifications & Certificates | Review | One-time |
| Enhanced DBS Certificate | Certificate number | 3-year |

### Document Status Badges

| Status | Colour | Meaning |
|--------|--------|---------|
| Missing | Rose | Not uploaded |
| Pending | Amber | Awaiting review |
| Verified | Green | Approved |
| Expiring | Orange | Within 30 days |
| Expired | Rose | Past expiry |

### Policies to Acknowledge (Stage 4)

1. Client Referral & Allocation Process
2. GDPR & Confidentiality Requirements
3. Cancellation Policy
4. Invoicing & Payment Process
5. Safeguarding Policy
6. Complaints Procedure

### Data Responsibility Matrix (Stage 5)

| Data Type | Eden | Shared | Associate |
|-----------|------|--------|-----------|
| Client Referral Forms | ✓ | | |
| Client Payment Details | ✓ | | |
| Client Contact Details | | ✓ | |
| Session Booking Records | | ✓ | |
| Clinical Notes | | | ✓ |
| Supervision Records | | | ✓ |

---

## 5. UCID SYSTEM

**Format:** `TYPE-YYSEQ`

| Type | Example | Description |
|------|---------|-------------|
| ASC | ASC-2401 | Associate |
| CLI | CLI-2507 | Client |
| SES | SES-2501 | Session |
| INV | INV-2503 | Invoice |

UCIDs use monospace font (`--font-mono`) in the UI.

---

## 6. PORTAL ARCHITECTURE

### Gateway Cards (Command Centre)

| Gateway | Icon | Drills Down To |
|---------|------|----------------|
| Clients | Users | Full client list with pipeline filter |
| Associates | User Check | Associate grid with status |
| Schedule | Calendar | Week/month calendar view |
| Finance | Wallet | Revenue, invoices, credits |
| Actions | Alert Circle | Friction Feed (exceptions only) |
| Messages | Mail | Inbox with unread count |

### Panel Architecture

**Associate Detail Panel (7 Tabs)**
1. Contact - Email, phone, address
2. Sessions - Upcoming and past
3. Contracts - Agreement status
4. Finance - Earnings, invoices
5. Inbox - Direct messages
6. Clients - Pipeline strip + client list
7. Onboarding - Progress tracker (NEW)

**Client Detail Panel (5 Tabs + Pipeline)**
1. Contact - Email, phone, referral source
2. Sessions - History and upcoming
3. Finance - Payments, credits
4. Notes - Internal notes
5. Timeline - Activity log
+ Pipeline tracker at top (7-stage journey)

### Responsive Patterns

| Screen | Pattern |
|--------|---------|
| Desktop | Side Panel (slides from right) + 3-column grid |
| Mobile | Bottom Sheet (slides from bottom) |

---

## 7. FRICTION FEED (Action Centre)

The Friction Feed shows **only exceptions** requiring attention. When everything is fine, users see "All Clear!"

### Alert Priority

| Colour | Priority | Examples |
|--------|----------|----------|
| Rose | Urgent | Expired documents, compliance gaps |
| Amber | Warning | Overdue follow-ups, pending reviews |
| Blue | Information | Unread messages, new leads |

### Triage Triggers

| Trigger | Alert Level |
|---------|-------------|
| Document expired | Rose |
| Document expiring (30 days) | Amber |
| Inquiry >24hrs no response | Amber |
| Client inactive >30 days | Amber |
| Unread message >48hrs | Blue |
| Supervision overdue | Rose |
| Supervision due soon (7 days) | Amber |
| DBS check overdue | Rose |
| DBS check due soon (30 days) | Amber |
| ICO not registered | Rose |
| ICO renewal due (30 days) | Amber |

---

## 8. CLINICAL GOVERNANCE ("Silent Auditor")

Eden bears vicarious responsibility under BACP, UKCP, and HCPC guidelines. The Clinical Governance module tracks compliance without surveillance.

### Supervision Tracker

| Field | Type | Notes |
|-------|------|-------|
| Supervisor_Name | Text | Required |
| Supervisor_Accreditation | Text | e.g., "BACP Registered" |
| Supervision_Frequency | Select | Weekly, Fortnightly, Monthly |
| Last_Supervision_Confirmed | Date | Updated by associate |
| Supervision_Due_Date | Formula | Calculated from frequency |
| Supervision_Status | Formula | Current, Due Soon, Overdue |

**Status Logic:**
- **Current**: Due date is >7 days away
- **Due Soon**: Due date is within 7 days
- **Overdue**: Due date has passed

### DBS Update Service

| Field | Type | Notes |
|-------|------|-------|
| DBS_Certificate_Number | Text | Original certificate number |
| DBS_Certificate_Date | Date | Date of original certificate |
| DBS_Update_Service_ID | Text | Subscription ID (if enrolled) |
| DBS_Update_Service_Enrolled | Checkbox | True if subscribed (£13/year) |
| DBS_Last_Checked | Date | Last annual check date |
| DBS_Next_Check_Due | Formula | Annual (if enrolled) or 3-year |
| DBS_Status | Formula | Valid, Renewal Soon, Expired |

**Status Logic:**
- **Valid**: Check due date is >30 days away
- **Renewal Soon**: Check due within 30 days
- **Expired/Check Due**: Check due date has passed

### ICO Registration

| Field | Type | Notes |
|-------|------|-------|
| ICO_Registration_Number | Text | Format: ZA****** or ZB****** |
| ICO_Registration_Verified | Checkbox | Manually verified by admin |
| ICO_Expiry_Date | Date | Annual renewal date |
| ICO_Status | Formula | Valid, Renewal Due, Expired, Not Registered, Pending |

**Onboarding Gate:** ICO Registration is REQUIRED in Stage 2 (Documents). Associates cannot progress without providing their ICO number.

### Visual States

| Status | Card Background | Icon Background | Friction Feed |
|--------|-----------------|-----------------|---------------|
| Current/Valid | Mint | Eden Green light | Not shown |
| Due Soon/Renewal Soon | Mint + amber border | Amber light | Amber item |
| Overdue/Expired | Soft red (#FEF2F2) | Rose light | Rose item |

---

## 9. WEALTH LAB (Financial Hub)

The Wealth Lab provides financial simulations for associates:

- **Efficiency Simulator**: Dividend vs pension remuneration choices
- **ISA Bridge Gap Tracker**: Tax-efficient savings planning
- **Tax Reclamation Visualisation**: Show potential savings

### Key Formula: True Cash

```
True Cash = Bank Balance - Unspent Credits - 25% Tax Reserve
```

### Revenue Split

Eden operates a **69/31 split**:
- Associate receives: 69%
- Eden retains: 31%

---

## 9. TECHNICAL STACK

| Layer | Technology |
|-------|------------|
| Frontend | React 18 + TypeScript |
| Styling | Tailwind CSS |
| Components | shadcn/ui |
| Icons | Lucide React (1.5px stroke) |
| Database | Airtable |
| Automation | Make.com |
| Email | MS365 Graph API |
| Payments | Stripe (via Squarespace) |
| Accounting | QuickBooks |
| Hosting | Vercel |
| Auth | Squarespace Member Areas |

---

## 10. IMPLEMENTATION CHUNKS

| Chunk | Feature |
|-------|---------|
| 1-3 | Foundation, Header, Sidebar |
| 4 | Gateway Cards (Command Centre) |
| 5-6 | Schedule, Client Cards |
| 7 | Associate (7 tabs) + Client (5 tabs + pipeline) panels |
| 8 | Utility panels |
| 9-10 | Responsive, Accessibility |
| 11 | Wealth Lab |
| 12 | Friction Feed |

---

## 11. MAKE.COM AUTOMATIONS

| Trigger | Action |
|---------|--------|
| New inquiry | Create client record, start 24hr clock |
| Client stage change | Update Airtable, notify if needed |
| 24hrs before session | Reminder email |
| Session completed | Move to Follow-Up |
| 48hrs after session | Feedback request |
| Document uploaded | Notify admin for review |
| Document verified | Confirm to associate |
| Document expiring (30 days) | Reminder email |
| Document expired | Create friction item |
| Supervision confirmed | Update Last_Supervision_Confirmed |
| Supervision overdue | Create friction item, soft reminder |
| DBS check marked | Update DBS_Last_Checked (admin only) |
| DBS renewal due (30 days) | Reminder email |
| ICO expiring (30 days) | Reminder email |

---

## 12. AIRTABLE SCHEMA

### Tables

- **Associates** - Primary client records, onboarding status
- **Clients** - End clients with pipeline stage
- **Sessions** - Booking records
- **Invoices** - Financial transactions
- **Documents** - Compliance tracking
- **Portal_Access_Log** - Security audit

### Key Fields

| Table | Field | Purpose |
|-------|-------|---------|
| Associates | UCID | Primary key (ASC-YYSEQ) |
| Associates | Status | Active/Paused/Offboarded |
| Associates | Onboarding_Stage | 1-6 (Welcome to Active) |
| Associates | Capacity_Percent | Availability indicator |
| Associates | Supervisor_Name | Clinical supervision contact |
| Associates | Supervision_Frequency | Weekly/Fortnightly/Monthly |
| Associates | Last_Supervision_Confirmed | Date of last confirmed supervision |
| Associates | Supervision_Status | Formula: Current/Due Soon/Overdue |
| Associates | DBS_Certificate_Number | Enhanced DBS certificate |
| Associates | DBS_Update_Service_Enrolled | Boolean: using annual service |
| Associates | DBS_Last_Checked | Date of last check |
| Associates | DBS_Status | Formula: Valid/Renewal Soon/Expired |
| Associates | ICO_Registration_Number | ICO data controller registration |
| Associates | ICO_Registration_Verified | Boolean: admin verified |
| Associates | ICO_Expiry_Date | Annual renewal date |
| Associates | ICO_Status | Formula: Valid/Renewal Due/Expired/Not Registered |
| Clients | Pipeline_Stage | 1-7 (Inquiry to Ongoing) |
| Clients | Assigned_Associate | Link to Associates |

---

## 13. ACCESSIBILITY REQUIREMENTS

- WCAG 2.1 AA compliance
- Keyboard navigation support
- 44px minimum touch targets on mobile
- All images have alt text
- Semantic HTML elements
- No colour-only indicators (always pair with text/icon)

---

## 14. RELATED DOCUMENTS

| Document | Location | Purpose |
|----------|----------|---------|
| ADR-001 | docs/decisions/ | Authentication architecture |
| PROJECT_CONTEXT | root | Human-readable philosophy |
| CLAUDE.md | root | AI development instructions |
| EDEN_STATUS.txt | root | Session handoff |

---

*This document consolidates Eden Portal Strategy v3, Design Specification v2.2, and Authentication Strategy v1.0*
