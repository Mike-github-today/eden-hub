# ARCHITECTURE DECISIONS

This document records significant architectural decisions made during Eden Hub Portal development.

---

## ADR-002: Clinical Governance as "Silent Auditor"

**Date:** 19 January 2026
**Status:** Accepted
**Context:** Clinical Governance Implementation

### Background

Eden bears vicarious responsibility under BACP, UKCP, and HCPC guidelines for ensuring associates maintain professional standards. This includes:
- Regular clinical supervision
- Valid DBS certification
- ICO registration for data controllers

### Decision

Implement clinical governance tracking as a "Silent Auditor" - the system passively monitors compliance without surveillance or hard blocks.

### Design Principles Applied

| Principle | Implementation |
|-----------|----------------|
| **Passive Monitoring** | Status calculated automatically from dates, no manual status updates required |
| **Soft Enforcement** | Amber indicators for "due soon", red only when overdue - never blocks associate actions |
| **Silent Admin** | Associates confirm supervision with one tap, admin verification happens behind scenes |
| **Friction Feed Integration** | Compliance issues appear as gentle reminders, not warnings |

### Technical Approach

1. **Status Formulas** - Mirror Airtable formula logic in JavaScript for prototype
2. **Three Compliance Cards** - Supervision, DBS, ICO in dedicated Compliance Section
3. **Onboarding Gate** - ICO required for Stage 2 completion (soft gate - shows warning, doesn't block)
4. **Visual States** - Green (current), Amber (due soon), Soft Red (overdue) - never aggressive red

### Alternatives Considered

| Alternative | Why Rejected |
|-------------|--------------|
| Hard blocks for non-compliance | Contradicts stewardship philosophy - associates are clients, not employees |
| Dashboard of all compliance metrics | "Dashboard theatre" - shows too much, creates anxiety |
| Email-only reminders | Misses opportunity for in-portal visibility and one-tap actions |
| Separate compliance module | Compliance is part of associate identity, belongs in profile |

### Consequences

**Positive:**
- Associates feel supported, not surveilled
- Compliance tracking is invisible until action needed
- One-tap confirmation reduces friction
- Admin overhead reduced through automation readiness

**Negative:**
- Associates could ignore soft warnings (acceptable risk given stewardship philosophy)
- No hard enforcement means ultimate responsibility remains with Mike/Maryanne

### Related

- See EDEN_MASTER.md Section 8 for data schema
- See EDEN_STATUS.txt for implementation details

---

## ADR-001: Squarespace Member Areas for Authentication

**Date:** January 2026
**Status:** Accepted
**Location:** docs/decisions/ADR-001.md (if exists) or documented in EDEN_MASTER.md

### Summary

Use Squarespace Member Areas for authentication rather than building custom auth, leveraging existing website infrastructure and reducing development complexity.

---

*Add new decisions above this line*
