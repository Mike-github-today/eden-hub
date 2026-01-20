# Eden Portal - Security & GDPR Compliance

**Version:** 1.0
**Last Updated:** January 2026
**Legal Basis:** GDPR (EU) 2016/679, Data Protection Act 2018 (UK)
**Review Cycle:** Quarterly or when data handling changes

---

## Core Principle: Data Minimisation

Eden Portal is designed with GDPR's data minimisation principle at its core. We only collect and process data that is strictly necessary for business operations.

### What Eden Stores (Permitted)

| Data Type | Purpose | Legal Basis |
|-----------|---------|-------------|
| Associate business information | Practice management | Legitimate interest |
| Associate contact details | Communication | Contract performance |
| Associate bank details | Payment processing | Contract performance |
| Session counts and revenue | Financial reporting | Contract performance |
| Compliance status (supervision, DBS, ICO) | Regulatory compliance | Legal obligation |
| Client enquiry metadata | Referral management | Legitimate interest |
| Invoices and payment records | Financial records | Legal obligation |

### What Eden NEVER Stores (Prohibited)

| Data Type | Why Excluded | Associate Responsibility |
|-----------|--------------|-------------------------|
| Clinical notes | Special Category Data (GDPR Art. 9) | Stored in associate's own systems |
| Session content | Health information | Associate's clinical responsibility |
| Detailed health information | Special Category Data | Associate's clinical records |
| Therapy session summaries | Health information | Associate's case notes |
| Diagnostic information | Special Category Data | Associate's clinical systems |

**This is a feature, not a limitation:** *"Eden never sees your clinical notes. Your therapeutic relationships remain entirely in your own systems."*

---

## Data Responsibility Matrix

| Data Type | Eden | Shared | Associate |
|-----------|:----:|:------:|:---------:|
| Client Referral Forms | ✓ | | |
| Client Payment Details | ✓ | | |
| Client Contact Details | | ✓ | |
| Session Booking Records | | ✓ | |
| Clinical Notes | | | ✓ |
| Supervision Records | | | ✓ |

---

## Portal Security Implementation

### Session Management

| Feature | Implementation | Standard |
|---------|---------------|----------|
| Session timeout | 30 minutes of inactivity | OWASP recommendation |
| Warning before timeout | 5 minutes countdown | User experience |
| Auto-logout | Forced logout after timeout | Security requirement |
| Activity detection | Mouse, keyboard, scroll, touch | Comprehensive tracking |
| Data clearing | All PII cleared on logout | GDPR compliance |

### Storage Compliance

| Storage Type | PII Permitted | Implementation |
|--------------|:-------------:|----------------|
| localStorage | No | PII validation on init |
| sessionStorage | Limited | Cleared on logout |
| Memory | Runtime only | Cleared on logout |
| Cookies | Session only | No persistent PII |

### Data Masking

| Data Type | Masking Pattern | Example |
|-----------|----------------|---------|
| Bank account | `•••• •••• •••• XXXX` | `•••• •••• •••• 1234` |
| DBS certificate | `****XXXX` | `****7890` |
| ICO registration | Full visibility | `ZA123456` |
| Email | `X***X@domain` | `j***n@email.com` |

### Error Message Sanitisation

All error messages shown to users are sanitised to prevent information disclosure:

| Scenario | Internal Log | User Message |
|----------|-------------|--------------|
| Database error | Full stack trace | "Unable to load data. Please try again." |
| Not found | "ID ASC-2501 not found" | "Resource not found." |
| Auth failure | "Token expired at..." | "Please log in again." |
| Network error | Full response | "Connection issue. Please check your network." |

---

## Make.com Security Configuration

### Data Redaction Settings

All Make.com scenarios handling PII must have:

1. **"Data is confidential"** enabled in scenario settings
2. **Log level** set to "Errors only" (not "All runs")
3. **Webhook validation tokens** implemented

### Scenarios Requiring Data Redaction

```
[EDEN] Associate Onboarding - Stage X    → Data Redaction: ON
[EDEN] Referral Broadcast                → Data Redaction: ON
[EDEN] Payment Processing                → Data Redaction: ON
[EDEN] Compliance Check Trigger          → Data Redaction: ON
[EDEN] Document Upload Handler           → Data Redaction: ON
```

### Webhook Security

All webhooks must:
1. Use HTTPS (Make.com default)
2. Include verification token in headers
3. Validate origin before processing

---

## Airtable Security Configuration

### Sensitive Fields

| Field | Visibility | UI Masking |
|-------|------------|------------|
| `Bank_Account_Number` | Restricted | Show last 4 digits only |
| `Sort_Code` | Restricted | Show last 2 digits only |
| `Email` | Full | Full visibility needed |
| `Phone` | Full | Full visibility needed |
| `DBS_Certificate_Number` | Restricted | Masked in UI |

### API Security

- API keys NEVER exposed in frontend code
- All Airtable calls go through Make.com (backend proxy)
- Rate limit awareness: 5 requests/second per base

### Data Location Notice

> Eden Portal uses Airtable for operational business data (invoices, compliance tracking, session counts). Clinical notes and health information are explicitly excluded from Eden systems and remain in associate's own clinical management tools. Airtable data is stored in US data centres under standard contractual clauses.

---

## Referral Broadcast System

### Minimal Data in Broadcasts

Only essential information is included in referral broadcasts:

**Included:**
- First name only (not full name)
- General enquiry type ("couples therapy", "anxiety support")
- Preferred session times
- Location preference (area/online)

**Excluded:**
- Detailed presenting issues
- Medical history
- Previous therapy experience
- Full contact details

### Broadcast Template

```
New Enquiry Available

Name: [First Name]
Type: [Service Category]
Availability: [Preferred Times]
Location: [Area/Online]

Interested? Accept to receive full details.
```

### Data Handoff Rules

1. Full client details only shared AFTER associate accepts referral
2. Acceptance logged with timestamp for audit
3. Unaccepted broadcasts auto-expire after 48 hours

---

## GDPR Rights Implementation

### Right to Access (Subject Access Request)

**Process:**
1. Receive request via email or portal
2. Verify identity of requester
3. Compile data from:
   - Airtable: Associate record, linked invoices, session records
   - Make.com: Scenario execution logs (redacted if configured)
4. Provide within **30 days**

**Data Export Format:** JSON or PDF, as requested

### Right to Erasure

**Process:**
1. Receive verified deletion request
2. Delete Airtable record and all linked records
3. Document the deletion request and completion
4. Make.com logs auto-expire (30 days)

**Retention exceptions:**
- Financial records (7 years - UK tax requirements)
- Compliance audit trail (anonymised)

### Right to Rectification

Associates can update their information directly through the portal. Admin corrections logged for audit.

### Right to Data Portability

Export available in standard formats (JSON, CSV) via admin request.

---

## Data Retention Policy

### Associate Data

| Status | Retention Period | Action |
|--------|-----------------|--------|
| Active associates | While relationship active | Full data retained |
| Inactive associates | 7 years | Required for UK tax/audit |
| After 7 years | Delete or anonymise | Remove PII, keep statistics |

### Enquiry Data

| Status | Retention Period | Action |
|--------|-----------------|--------|
| Accepted and converted | Becomes client record | Associate's responsibility |
| Not accepted | 90 days | Auto-delete |
| Rejected | Immediate | Delete on rejection |

### Financial Records

| Type | Retention Period | Legal Basis |
|------|-----------------|-------------|
| Invoices | 7 years | UK tax law |
| Payment records | 7 years | UK tax law |
| Payout history | 7 years | UK tax law |

---

## Quarterly Audit Checklist

| Item | Check | Last Verified | Next Review |
|------|:-----:|---------------|-------------|
| Make.com data redaction enabled | ☐ | | |
| No clinical note fields in Airtable | ☐ | | |
| Webhook tokens rotated | ☐ | | |
| Inactive enquiries purged | ☐ | | |
| SAR process tested | ☐ | | |
| Session timeout working | ☐ | | |
| Error messages sanitised | ☐ | | |
| No PII in localStorage | ☐ | | |
| Bank details masked | ☐ | | |

---

## Incident Response

### Data Breach Protocol

1. **Identify** - Assess scope and nature of breach
2. **Contain** - Prevent further data exposure
3. **Notify ICO** - Within 72 hours if required
4. **Notify affected** - If high risk to individuals
5. **Document** - Full incident report
6. **Review** - Implement preventive measures

### Contact

**Data Protection queries:** [privacy@edenrelationships.co.uk]
**ICO Registration:** [ZAxxxxxx]

---

## Version History

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | January 2026 | Initial security & GDPR implementation |

---

*This document should be reviewed quarterly and updated whenever data handling processes change.*
