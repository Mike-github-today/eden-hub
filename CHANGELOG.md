# CHANGELOG

All notable changes to Eden Hub Portal.

---

## [Unreleased]

### Planned
- Airtable live data integration
- Make.com webhook connections
- Squarespace authentication integration
- Mobile app wrapper

---

## [0.6.0] - 2026-01-18

### Added
- **Three-Dots Menu Standardisation (Chunk 6)**
  - Removed kebab menus from all list/status cards
  - Menus now appear ONLY in detail view headers
  - Role-aware menu items (Admin vs Associate permissions)
  - Divider support in dropdown menus
  - Dynamic menu population based on `currentUserRole`
  - New icons: download, bell for contract actions

### Changed
- Simplified `renderStatusCard` function (removed ~70 lines)
- Menu configuration now per entity type and role
- Associate detail menu hidden for associate role (no self-actions)

### Removed
- Kebab menu CSS (~130 lines)
- Kebab menu JavaScript functions (~75 lines)

---

## [0.5.1] - 2026-01-18

### Added
- **Empty States (Chunk 5)**
  - "Garden in Bloom" empty state illustrations
  - Contextual empty messages per module and role
  - Animated leaf/growth SVG illustrations
  - Role-aware empty state actions

---

## [0.5.0] - 2026-01-18

### Added
- **Action Centre Summary Grid (Chunk 4)**
  - Quick-glance friction summary cards
  - Priority-based grouping (Urgent, Warning, Info)
  - Filter tabs by category
  - Clickable summary cards navigate to filtered view

---

## [0.4.0] - 2026-01-17

### Added
- **Unified Detail View Pattern (Chunk 3)**
  - Consistent panel architecture across all entity types
  - Tab-based navigation within panels
  - Shared header component with avatar, name, UCID
  - Entity-specific tab configurations
  - Pipeline tracker integration for clients

### Fixed
- Navigation bug fixes for panel state management
- Back button behaviour in nested views

---

## [0.3.0] - 2026-01-14

### Added
- **Referral System Implementation**
  - Admin referral workflow (New → Triage → Broadcast → Allocate)
  - Associate interest expression interface
  - Referral status badges (New, Broadcasting, Pending, Accepted, Declined)
  - Specialisation matching system (24 specialisations)
  - Referral stats dashboard with filter cards
  - Referral detail panel with context-aware content
  - Expression tracking for associate interest

- **Progress Stepper Component**
  - Reusable stepper for multi-stage workflows
  - Visual step indicators with completion states
  - Click-to-navigate between stages

---

## [0.2.0] - 2026-01-10

### Added
- **Financial Vitality Hub (Wealth Hub)**
  - True Cash calculation and display
  - Cash Density module with 3-month projection
  - Tax Intelligence (Pre-VAT mode with threshold tracking)
  - Payout Cockpit for admin payment management
  - Wealth Lab Simulator (dividend vs pension planning)
  - System Health monitoring placeholder
  - Admin Payment Tracker with table view
  - Payout Pipeline grid with associate cards
  - 69/31 revenue split visualization

- **Associate Earnings View**
  - Earnings hero card with progress bar
  - Breakdown cards (Awaiting, Ready, Paid)
  - Session list grouped by status
  - Collapsible payout history

- **Schedule/Calendar Module**
  - Monthly calendar with navigation
  - Today's sessions list
  - Session detail panel
  - Session cards with status indicators (Confirmed/Pending/Cancelled)
  - Add session modal placeholder

---

## [0.1.0] - 2026-01-06

### Added
- **Core Design System (Eden Calm)**
  - CSS custom properties (no grey palette)
  - Eden Mint (#F4F7F6), Eden Green (#2D5F4D), Pure White (#FFFFFF)
  - Alert colours: Amber (#F59E0B), Rose (#EF4444), Blue (#3B82F6)
  - Component tokens (radius, shadows, transitions)
  - iOS Safe Area support
  - System font stack

- **Layout & Navigation**
  - Fixed sidebar (260px) with Eden branding
  - Side panel (450px) for desktop detail views
  - Bottom sheet (85vh) for mobile detail views
  - Mobile header with hamburger menu
  - Responsive breakpoint at 768px
  - Role toggle button (Admin ↔ Associate)
  - Access denied notifications for restricted views

- **Associates Module**
  - ID card grid with capacity indicators
  - Support mode badges (Independent/Supported)
  - 7-tab detail panel:
    - Overview (quick stats)
    - Contact (personal + emergency)
    - Sessions (timeline)
    - Contracts (status cards)
    - Finance (earnings breakdown)
    - Inbox (messages)
    - Clients (pipeline + list)
  - Capacity gauge view
  - Associate inbox view

- **Clients Module**
  - Client card grid with stage indicators
  - 7-stage pipeline tracker (Inquiry → Ongoing)
  - Client detail panel with 5 tabs + pipeline
  - Mini-cards in associate view with filters
  - Stage-based filtering

- **Action Centre (Friction Feed)**
  - Exception-only display philosophy
  - Friction items with priority levels
  - Resolution drawer for quick actions
  - "All Clear!" success state
  - Category filtering

- **Contracts Module**
  - Contract grid with status filters
  - Contract detail panel
  - Status badges (Signed/Pending)

- **Messages/Inbox**
  - Message list with unread indicators
  - Message viewer panel
  - Reply/Archive actions
  - Compose button

- **Support Module**
  - Support links grid
  - Emergency contacts
  - Help resources

- **CPD Module**
  - Activities list
  - Progress tracking placeholder

- **Mock Data**
  - 7 associates with full profiles
  - 20+ clients with stage assignments
  - 4 referrals with expression tracking
  - Session records for finance
  - Friction items
  - Contracts
  - Messages

---

## Version Numbering

- **Major (X.0.0)**: Breaking changes or major feature launches
- **Minor (0.X.0)**: New features, significant additions
- **Patch (0.0.X)**: Bug fixes, minor updates

---

## Implementation Approach

The portal is built as a **single-file HTML prototype** (~900KB) to ensure:
- Complete understanding of every line of code
- No "black box" components
- Clear migration path to React when ready
- Rapid iteration without build tooling

---

*See EDEN_STATUS.txt for detailed session-by-session progress*
