# 🌍 University of Dubai — Short Research Visits System (SRVS)
## Screen Layout & Design Specification Document · v1.0

---

> **Document Status:** Draft — For Review  
> **Version:** 1.0  
> **Date:** June 2026  
> **Prepared by:** Research Affairs  
> **Audience:** IT Dept  
> **Classification:** Confidential — Internal Use Only  
> **Reference PRD:** SRVS PRD v1.0
---

## 📋 Table of Contents

1. [Design System & Global Standards](#1-design-system--global-standards)
2. [Global Shell & Navigation](#2-global-shell--navigation)
3. [Screen 01 — Login Page](#3-screen-01--login-page)
4. [Screen 02 — Faculty: Home Dashboard](#4-screen-02--faculty-home-dashboard)
5. [Screen 03 — Faculty: New Application Form](#5-screen-03--faculty-new-application-form)
6. [Screen 04 — Faculty: Application Status & Detail View](#6-screen-04--faculty-application-status--detail-view)
7. [Screen 05 — Faculty: Post-Visit Obligation Tracker](#7-screen-05--faculty-post-visit-obligation-tracker)
8. [Screen 06 — Approver: Home Dashboard (Dean · Director of Research · VPAA · President)](#8-screen-06--approver-home-dashboard-dean--director-of-research--vpaa--president)
9. [Screen 07 — Approver: Pending Approvals Queue](#9-screen-07--approver-pending-approvals-queue)
10. [Screen 08 — Approver: Single Application Review](#10-screen-08--approver-single-application-review)
11. [Screen 09 — Approver: All Applications View](#11-screen-09--approver-all-applications-view)
12. [Screen 10 — Departmental Quota Heat Map](#12-screen-10--departmental-quota-heat-map)
13. [Screen 11 — Post-Visit Compliance Dashboard](#13-screen-11--post-visit-compliance-dashboard)
14. [Screen 12 — Executive Dashboard (VPAA & President)](#14-screen-12--executive-dashboard-vpaa--president)
15. [Screen 13 — HR: Home & Eligibility Feed](#15-screen-13--hr-home--eligibility-feed)
16. [Screen 14 — System Admin: Home & User Management](#16-screen-14--system-admin-home--user-management)
17. [Screen 15 — System Admin: Department Headcounts & Quota Configuration](#17-screen-15--system-admin-department-headcounts--quota-configuration)
18. [Screen 16 — System Admin: Workflow & Notification Configuration](#18-screen-16--system-admin-workflow--notification-configuration)
19. [Screen 17 — System Admin: Audit Log](#19-screen-17--system-admin-audit-log)
20. [Screen 18 — System Admin: Academic Year & Summer Session Management](#20-screen-18--system-admin-academic-year--summer-session-management)
21. [Screen 19 — Notifications Centre (All Roles)](#21-screen-19--notifications-centre-all-roles)
22. [Screen 20 — Profile, Settings & Delegation (All Roles)](#22-screen-20--profile-settings--delegation-all-roles)
23. [Component Library Reference](#23-component-library-reference)
24. [Role-to-Screen Access Matrix](#24-role-to-screen-access-matrix)

---

## 1. Design System & Global Standards

### 1.1 Colour Palette

| Token | Hex | Usage |
|---|---|---|
| `--ud-navy` | `#1B3A6B` | Sidebar background, primary headings, header text |
| `--ud-gold` | `#C8972A` | Accent borders, active states, CTA highlights, dividers |
| `--ud-blue-mid` | `#2563A8` | Links, secondary buttons, icon fills |
| `--ud-blue-light` | `#EBF3FB` | Table row hover, card backgrounds, info banners |
| `--ud-teal` | `#1E8A85` | Compliance "in progress" states, post-visit tracker accents |
| `--ud-white` | `#FFFFFF` | Page background, card backgrounds |
| `--ud-grey-bg` | `#F5F7FA` | Page canvas background, alternate table rows |
| `--ud-grey-border` | `#D1D9E6` | All borders, dividers, input outlines |
| `--ud-text-dark` | `#1A1A2E` | Primary body text |
| `--ud-text-mid` | `#4A4A6A` | Secondary text, labels, captions |
| `--ud-text-light` | `#8A8AAA` | Placeholder text, disabled states, timestamps |

**Status Colours (always used with a matching text label — never colour alone):**

| Status | Background | Text / Border | Usage |
|---|---|---|---|
| Draft | `#F0F0F0` | `#6B6B6B` | Application saved, not submitted |
| Pending (any stage) | `#FFF8E1` | `#B8860B` | Awaiting approver action |
| Approved | `#E8F5E9` | `#1A7A4A` | Final Presidential approval complete |
| Rejected | `#FDEDED` | `#C0392B` | Rejected at any stage |
| Returned | `#FFF3E0` | `#E65100` | Sent back to faculty for revision |
| Waitlisted | `#EDE7F6` | `#5E35B1` | Department at 25% cap — queued for a slot |
| Eligible | `#E8F5E9` | `#1A7A4A` | Auto-check passed |
| Blocked | `#FDEDED` | `#C0392B` | Auto-check failed — cites policy clause |
| Overdue | `#FDEDED` | `#C0392B` | SLA or obligation deadline exceeded (+ red left border on row) |

**Departmental Quota Heat Map scale (Section 12):**

| Range | Colour | Meaning |
|---|---|---|
| 0–14% | `#E8F5E9` (green) | Healthy headroom |
| 15–24% | `#FFF8E1` (amber) | Approaching the 25% cap |
| ≥ 25% | `#FDEDED` (red) | At or over cap — new applications blocked |

**Post-Visit Obligation status dots:**

| Status | Colour | Meaning |
|---|---|---|
| 🟢 Complete | `#1A7A4A` | Evidence submitted and accepted |
| 🟡 In Progress | `--ud-teal` `#1E8A85` | Within deadline, not yet due |
| 🔴 Overdue | `#C0392B` | Deadline passed without evidence |

---

### 1.2 Typography

| Style | Font | Size | Weight | Usage |
|---|---|---|---|---|
| Page Title | Calibri / Inter | 24px | 700 | Main screen heading |
| Section Heading | Calibri / Inter | 18px | 600 | Section titles within a page |
| Sub-heading | Calibri / Inter | 15px | 600 | Card titles, table section headers |
| Body | Calibri / Inter | 14px | 400 | All body text, form labels |
| Caption | Calibri / Inter | 12px | 400 | Timestamps, helper text, annotations |
| Button | Calibri / Inter | 14px | 600 | All button labels |
| Monospace | Courier New | 13px | 400 | Reference numbers (e.g. SRV-2026-CB-0017) |

---

### 1.3 Spacing & Layout Grid

- **Canvas background:** `--ud-grey-bg` (`#F5F7FA`) — the page sits on a light grey canvas
- **Content area:** White cards on the grey canvas, `16px` padding inside cards
- **Card border radius:** `8px`
- **Card shadow:** `0 1px 4px rgba(0,0,0,0.08)` — subtle, not heavy
- **Grid:** 12-column grid, `24px` gutters
- **Standard content max-width:** `1280px`, centred in the content area
- **Section spacing:** `24px` between major sections on a page
- **Form field height:** `40px` (inputs, selects, date pickers)
- **Button height:** `36px` standard, `40px` primary CTA

---

### 1.4 Button System

| Type | Style | Usage |
|---|---|---|
| **Primary** | Navy fill (`#1B3A6B`), white text, gold `2px` bottom border on hover | Main CTA — Submit, Approve, Save |
| **Secondary** | White fill, navy border, navy text | Supporting actions — Save Draft, Cancel, Back |
| **Danger** | Red fill (`#C0392B`), white text | Destructive — Reject, Delete, Close Academic Year |
| **Warning** | Orange fill (`#E65100`), white text | Return for Revision |
| **Ghost** | Transparent, navy text, navy border on hover | Tertiary — Export, View, Download |
| **Icon button** | Icon only, no label, navy icon, light grey hover circle | Compact actions in table rows |

---

### 1.5 Form Elements

- **Input fields:** White background, `1px` solid `--ud-grey-border`, `8px` border radius, `14px` font, gold left border `2px` on focus
- **Required field indicator:** Red asterisk `*` after the label
- **Inline validation error:** Red text below the field (`12px`), red border on the field
- **Inline validation success:** Green checkmark icon inside the field (right side)
- **Helper text:** Grey caption below the field (`12px`), appears always (not just on error) — often cites the relevant policy clause
- **Auto-populated fields:** Light blue tint background (`--ud-blue-light`), padlock icon on the right, tooltip: "Auto-filled from your profile"
- **Disabled fields:** `#F5F7FA` background, `--ud-text-light` text
- **Auto-computed eligibility fields:** Cannot be edited by the faculty member under any circumstance; always rendered with a small "🔒 System-verified" tag rather than the standard padlock tooltip, to distinguish a policy gate from a simple convenience auto-fill

---

### 1.6 Table Standards (applies to all tables across the platform)

- **Column headers:** `--ud-navy` background, white text, `14px` bold, `12px` padding
- **Rows:** Alternating white / `--ud-grey-bg`, `48px` row height
- **Hover state:** `--ud-blue-light` background on hover
- **Row click:** Entire row is clickable and navigates to the detail view
- **Column sorting:** Up/down arrow icon in header; active sort shown with gold filled arrow
- **Column filtering:** Filter icon (funnel) in header; clicking opens a small dropdown or text input below the header
- **Global search bar:** Positioned above the table, full width of the table, with a search icon on the left
- **Pagination:** Bottom of the table — "Showing 1–20 of 47 results" on the left, page navigation buttons on the right (Previous · 1 · 2 · 3 · Next), page size selector (20 / 50 / 100 per page)
- **Overdue rows:** Red left border `4px` on the row + amber background
- **Empty state:** Centred icon + one-line message + primary action button (see Section 1.7)

---

### 1.7 Empty State Standard

When a table, list, or queue has no data:

```
[Icon — relevant to context, e.g. plane for applications, checklist for tasks]
No research visit applications found.
[Primary action button if applicable — e.g. "Start New Application"]
```

- Icon: `48px`, `--ud-text-light` colour
- Message: `16px`, `--ud-text-mid`, centred
- Button: Primary style, centred below message

---

### 1.8 Status Badge Component

All status badges follow this pattern:

```
[● Coloured dot] [Status Label Text]
```

- Container: `4px` border radius, `6px 10px` padding
- Background and text colour per status table in Section 1.1
- Font: `12px`, `600` weight
- Always includes a text label — never colour alone

---

### 1.9 Policy Clause Citation Tag

A small recurring component used throughout SRVS wherever an automated decision needs to show its legal basis (a faculty member should never have to ask "why was I blocked?").

```
[📘 Clause H]
```

- `11px`, navy text on light blue chip, `4px` border radius
- Clicking it opens a tooltip with the plain-language summary of that clause
- Used on: eligibility checklist, blocked-submission banners, quota cap messages, post-visit non-compliance flags

---

## 2. Global Shell & Navigation

### 2.1 Layout Structure

The global shell is the persistent wrapper around all authenticated screens. It has three regions:

```
┌──────────────────────────────────────────────────────────────┐
│  TOP HEADER BAR                                              │
├──────────┬───────────────────────────────────────────────────┤
│          │                                                   │
│  LEFT    │   MAIN CONTENT AREA                               │
│ SIDEBAR  │                                                   │
│          │                                                   │
│          │                                                   │
└──────────┴───────────────────────────────────────────────────┘
```

---

### 2.2 Top Header Bar

**Height:** `56px`
**Background:** `--ud-white`
**Bottom border:** `2px` solid `--ud-gold`

**Left section (from left):**
- Sidebar collapse/expand toggle button — hamburger icon (`20px`), `--ud-navy`, `16px` left margin. Clicking toggles the sidebar between expanded (`240px`) and icon-only (`64px`) modes.
- UD Logo — horizontal lockup (logo + "University of Dubai" wordmark), `140px` wide, links to Home

**Centre section:**
- System name label: `"Short Research Visits System"`, `14px`, `--ud-text-mid`, non-clickable

**Right section (from right, `16px` right margin):**
- **User avatar + name:** Circular avatar (`32px`), user's full name (`14px`, `--ud-text-dark`), role label below name (`11px`, `--ud-text-light`). Clicking opens a small dropdown: My Profile · Sign Out
- **Divider:** `1px` vertical `--ud-grey-border`
- **Notification bell icon:** `22px`, `--ud-navy`. If unread notifications exist, a red badge with the count is shown (max "9+"). Clicking opens the notification dropdown (last 5, with "See all" link to full notifications page)
- **Divider**
- **Academic Year selector:** Dropdown showing the current summer session cycle (e.g. "Summer 2026"). Admin can change this; other roles see it read-only as context.

---

### 2.3 Left Sidebar

**Expanded width:** `240px`
**Collapsed width:** `64px` (icon-only mode)
**Background:** `--ud-navy`
**Transition:** `200ms ease` width animation

**Expanded state — each menu item:**
```
[Icon 20px]  [Label text 14px]         [Optional badge]
```
- Item height: `44px`
- Padding: `12px 16px`
- Text: white, `400` weight
- Icon: white, `20px`
- Hover: `rgba(255,255,255,0.08)` background
- Active (current page): gold left border `3px` + `rgba(200,151,42,0.15)` background + white bold text
- Optional badge: small pill (e.g. "3" pending approvals), gold background, navy text, `10px` font

**Collapsed state — each menu item:**
- Icon only, centred in `64px` width
- Tooltip on hover: shows the label in a small navy tooltip to the right

**Bottom of sidebar (always visible, expanded and collapsed):**
- Separator line
- Help & Support link (question mark icon)
- System version number (`v1.0`, `11px`, white at 40% opacity)

---

### 2.4 Sidebar Menu Items by Role

#### Faculty Member
| Icon | Label | Badge | Links to |
|---|---|---|---|
| 🏠 | Home | — | Faculty Home Dashboard |
| 📋 | My Applications | Count of active applications | My Applications list |
| ✈️ | New Application | — | Application Form (Step 1) |
| ✅ | Post-Visit Tasks | Count of overdue/pending tasks | Post-Visit Obligation Tracker |
| 👤 | Profile | — | Profile & Settings |

#### College Dean
| Icon | Label | Badge | Links to |
|---|---|---|---|
| 🏠 | Home | — | Approver Home Dashboard |
| ⏳ | Pending Approvals | Count of pending | Pending Approvals Queue |
| 📁 | All Applications | — | All Applications View (college scope) |
| 🗺️ | Department Quota | — | Departmental Quota Heat Map (college scope) |
| 📊 | Compliance Dashboard | Count of overdue obligations | Post-Visit Compliance Dashboard |
| 👤 | Profile | — | Profile & Settings |

#### Director of Research
| Icon | Label | Badge | Links to |
|---|---|---|---|
| 🏠 | Home | — | Approver Home Dashboard |
| ⏳ | Pending Approvals | Count of pending | Pending Approvals Queue |
| 📁 | All Applications | — | All Applications View (university-wide) |
| 🗺️ | Department Quota | — | Departmental Quota Heat Map (university-wide) |
| 📊 | Compliance Dashboard | Count of overdue obligations | Post-Visit Compliance Dashboard |
| 👤 | Profile | — | Profile & Settings |

#### VP of Academic Affairs / University President
| Icon | Label | Badge | Links to |
|---|---|---|---|
| 🏠 | Home | — | Approver Home Dashboard |
| ⏳ | Pending Approvals | Count of pending | Pending Approvals Queue |
| 📁 | All Applications | — | All Applications View (university-wide) |
| 🗺️ | Department Quota | — | Departmental Quota Heat Map |
| 📈 | Executive Dashboard | — | Executive Dashboard |
| 👤 | Profile | — | Profile & Settings |

#### HR Department
| Icon | Label | Badge | Links to |
|---|---|---|---|
| 🏠 | Home | — | HR Home Dashboard |
| 🔄 | Eligibility Feed | Count of flagged exceptions | Eligibility Feed Status |
| 👥 | Faculty Directory | — | Faculty Directory (read-only) |
| 👤 | Profile | — | Profile & Settings |

#### System Administrator
| Icon | Label | Badge | Links to |
|---|---|---|---|
| 🏠 | Home | — | Admin Home Dashboard |
| 👥 | User Management | — | User Management Screen |
| 🏢 | Department Headcounts | — | Headcounts & Quota Configuration |
| ⚙️ | Workflow Config | — | Workflow & Notification Configuration |
| 📋 | Audit Log | — | Audit Log Viewer |
| 📅 | Academic Year | — | Academic Year & Summer Session Management |
| 👤 | Profile | — | Profile & Settings |

---

### 2.5 Notification Dropdown (Bell Icon)

**Triggered by:** Clicking the bell icon in the top header bar
**Dimensions:** `360px` wide, max `480px` tall, scrollable
**Position:** Drops below the bell icon, right-aligned to the header right edge
**Shadow:** `0 4px 20px rgba(0,0,0,0.12)`

**Header of dropdown:**
```
Notifications                    [Mark all as read]
```

**Each notification item:**
```
[● Unread dot / empty]  [Title — bold 14px]                  [Timestamp]
                        [Body — 13px, --ud-text-mid, 2 lines max]
                        [Reference: SRV-2026-CB-0017]
```
- Unread items: white background, left border `3px --ud-gold`
- Read items: `--ud-grey-bg` background
- Hover: `--ud-blue-light` background
- Clicking a notification: marks as read + navigates to the relevant application or task

**Footer:**
```
[See all notifications →]
```
- Centred link, `14px`, `--ud-blue-mid`, navigates to full Notifications page

---

## 3. Screen 01 — Login Page

### 3.1 Purpose
Entry point for all users. Authenticates via UD Microsoft 365 SSO. No password field in the system itself.

### 3.2 Layout

**Background:** `--ud-white` full page

**Centred login card:**
- Width: `420px`
- Border radius: `12px`
- Shadow: `0 4px 24px rgba(0,0,0,0.10)`
- Padding: `48px`
- Border top: `4px` solid `--ud-gold`

**Inside the card (top to bottom):**

```
[UD Logo — centred, 160px wide]

[Vertical space: 24px]

University of Dubai
[16px, --ud-text-mid, centred]

Short Research Visits System
[22px, bold, --ud-navy, centred]

[Vertical space: 8px]

[Horizontal divider — --ud-gold, 40px wide, centred]

[Vertical space: 32px]

Welcome. Please sign in with your
University of Dubai account.
[14px, --ud-text-mid, centred, 2 lines]

[Vertical space: 24px]

[         Sign in with Microsoft 🔷        ]
[Primary button, full width, 44px height]
[Microsoft logo icon on left, "Sign in with Microsoft" text]
[Navy background, white text]

[Vertical space: 16px]

Having trouble signing in? Contact IT Support
[12px, --ud-text-light, centred, "IT Support" is a link]
```

**Below the card (page footer):**
```
© 2026 University of Dubai · Confidential — Internal Use Only
[12px, --ud-text-light, centred]
```

### 3.3 States

| State | Behaviour |
|---|---|
| Default | Card as above |
| Loading (after click) | Button shows spinner + "Signing in…" text, disabled |
| Error (SSO failure) | Red alert banner above the button: "Sign-in failed. Please try again or contact IT Support." |
| Session expired | Same page with an amber banner: "Your session has expired. Please sign in again." |

### 3.4 Annotations
- The page has no sidebar or header — it is a standalone pre-auth screen
- After successful SSO, the system checks the user's role in Active Directory and redirects to the appropriate Home Dashboard
- First-time login triggers a profile confirmation step (read-only review of AD-sourced fields) before reaching the dashboard

---

## 4. Screen 02 — Faculty: Home Dashboard

### 4.1 Purpose
The Faculty member's primary view after login. Shows application activity, post-visit obligations, and quick actions. This IS their home — no separate landing page.

### 4.2 Layout

**Page title:** `Home` (in breadcrumb area below header)

**Top area — Welcome bar:**
```
Good morning, Dr. Sara Al Bloushi 👋
[24px, --ud-navy, bold]
Here is your current research visit activity.
[14px, --ud-text-mid]
                                    [+ New Application]  [primary button, top-right]
```

---

**Row 1 — KPI Summary Cards (4 cards, equal width, across full content area):**

Each card:
- White background, `8px` border radius, `1px` border `--ud-grey-border`
- Gold top border `3px`
- `16px` padding
- Left: large number (`32px`, bold, `--ud-navy`), label below (`13px`, `--ud-text-mid`)
- Right: relevant icon (`32px`, `--ud-blue-light` circle background)

| Card 1 | Card 2 | Card 3 | Card 4 |
|---|---|---|---|
| Total Applications | Pending Approval | Approved Visits | Post-Visit Tasks Open |
| This academic record | Currently in workflow | All-time | Awaiting completion |

---

**Row 2 — Two columns:**

**Left column (65% width) — My Applications:**
- Section heading: `My Applications` + `[View all →]` link on the right
- Table with 5 most recent applications:

| Reference | Host Institution | Submitted | Status | Action |
|---|---|---|---|---|
| SRV-2026-CB-0017 | University of Manchester, UK | 12 Jun 2026 | [Pending Dean] | View |

- Columns: Reference (monospace), Host Institution, Submitted Date, Status (badge), Action (ghost button "View")
- All table standards from Section 1.6 apply
- "View all" link below the table

**Right column (35% width) — Action Required:**

Card titled `Action Required`:
- List of items needing attention, each item:
  ```
  [!] Post-visit obligation due — Univ. of Manchester
      Progress report due in 3 days
      [Complete Now →]
  ```
  - Orange left border `3px` for overdue items
  - Amber for due-soon items (within 3 days)
- If a draft is about to expire:
  ```
  [!] Draft expiring soon
      "SRV-DRAFT-0009" will be deleted in 3 days
      [Resume Draft →]
  ```
- If no items: Empty state — "No pending tasks. You're all caught up!"

---

**Row 3 — Application Pipeline Visual:**
- Section heading: `Approval Progress`
- For each active application, show a horizontal stepper:
  ```
  Application: University of Manchester, UK  [SRV-2026-CB-0017]
  ●━━━━●━━━━○━━━━○━━━━○
  Dean Dir.  VP  Pres.  Done
  [Completed in green ●] [Current in gold ●] [Upcoming in grey ○]
  ```
- Each dot is labelled below
- Current stage has a pulsing gold dot animation
- Up to 3 active applications shown; "View all" link if more

---

**Row 4 — Recent Notifications strip:**
- Section heading: `Recent Notifications`
- 3 most recent notification items (compact, no full dropdown)
- Each: icon · message · timestamp · "View" link
- `[See all notifications →]` link at the end

---

### 4.3 Sidebar Active State
`Home` item is active (gold left border, bold white text).

---

## 5. Screen 03 — Faculty: New Application Form

### 5.1 Purpose
Multi-step wizard for faculty to submit a Short Research Visit application. 7 sections (A–G), one section per step, with the eligibility engine running automatically before the form can be submitted.

### 5.2 Layout — Wrapper

**Page title area (below header):**
```
Breadcrumb: Home  >  My Applications  >  New Application
Page Title: New Research Visit Application
[14px caption below]: Reference will be assigned upon submission.
```

**Two-column layout:**
- **Left: Step Navigator (240px fixed, sticky)** — stays in place as the user progresses
- **Right: Active Step Content (fills remaining width)**

---

### 5.3 Left — Step Navigator Panel

White card, `8px` border radius, full page height sticky.

**Header:**
```
Application Progress
[14px, --ud-text-mid]
[Progress bar: thin gold bar, fills as steps complete]
Step 3 of 7 — Visit Details
[12px, --ud-text-light]
```

**Step list (each step is a row):**
```
[Connector line]
[●] A  Applicant Information     ✓ Complete
[●] B  Host Institution Details  ✓ Complete
[●] C  Visit Details             ← Current (gold, bold)
[○] D  Research Proposal & Output
[○] E  Eligibility Checklist
[○] F  Document Uploads
[○] G  Calendar & Coverage
```

Each step row:
- Height: `52px`
- Left: circle indicator (filled green ✓ = complete, filled gold = current, empty grey = upcoming)
- Vertical connector line between steps (grey, turns green as steps complete)
- Step letter + step name (`14px`)
- Completed steps show a green checkmark icon

**Below step list:**
```
[Save as Draft]  [secondary button, full width]
```
Annotation: Saves current progress without submitting. Drafts are retained for 90 days. Auto-save also triggers every 60 seconds.

---

### 5.4 Right — Step Content Area

Each step occupies this area. Navigation buttons are always at the bottom.

**Bottom action bar (sticky at bottom of content area):**
```
[← Back]          Step 3 of 7          [Save Draft]  [Next: Research Proposal →]
```
- Back: secondary button (hidden on Step 1)
- Next: primary button
- On Step 7 (final): Next becomes `[Submit Application]` primary button

---

### 5.5 Step A — Applicant Information

**Section heading:** `A. Applicant Information`
**Caption:** `These fields are automatically populated from your university profile. Please verify and confirm.`

All fields are auto-filled and locked (read-only with blue tint + padlock icon):

| Field | Value | Notes |
|---|---|---|
| Full Name | Dr. Sara Al Bloushi | From Active Directory |
| Employee ID | UD-FAC-2089 | From Active Directory |
| College | College of Business | From Active Directory |
| Department | Finance & Accounting | From Active Directory |
| Academic Rank | Associate Professor | From Active Directory |
| Submission Date | 12 Jun 2026 | System auto-set |

**Below fields:**
```
[i] Not correct? Contact HR to update your profile details.
[14px, --ud-text-mid, info icon, --ud-blue-mid]
```

---

### 5.6 Step B — Host Institution Details

**Section heading:** `B. Host Institution Details`

| Field | Type | Required | Notes |
|---|---|---|---|
| Host University Name | Text input | ✱ | |
| Country | Dropdown | ✱ | Searchable country list |
| City | Text input | ✱ | |
| World Ranking Tier | Selectable chips | — | QS Top 200 · THE Top 200 · ARWU Top 200 · Other — preference, not a hard requirement |
| Host has a program/policy for hosting international researchers? | Radio + description | ✱ | Yes / No + text field |
| Facilities & resources to be provided | Textarea + upload | ✱ | Supporting document optional |
| Collaborator Name | Text input | Conditional | Only if visit type (Step C) is Collaborative |
| Collaborator Bio | File upload | Conditional | Mirrors Section F requirement |

**Smart Ranking Verification widget (right side, collapsible panel `280px`):**
```
🏅 Ranking Verification
━━━━━━━━━━━━━━━━━━━━━━
University of Manchester
✅ Top 200 — Preferred
[Confirmed against QS World University
Rankings 2026]

[View ranking source ↗]
```
- Badge states: `✅ Top 200 — Preferred` (green) · `⚠️ Outside Top 200 — Requires Dean Justification` (amber) · `⏳ Verification Pending` (grey)
- This is informational only — it does not block submission, per policy preference rather than a hard rule

---

### 5.7 Step C — Visit Details

**Section heading:** `C. Visit Details`

| Field | Type | Required | Notes |
|---|---|---|---|
| Visit Type | Radio | ✱ | Individual Research · Collaborative Research |
| Planned Start Date | Date picker | ✱ | Must fall on/after the UD summer session start |
| Planned End Date | Date picker | ✱ | Must be on/before reporting-back-to-duty date |
| Duration | Calculated display | — | Auto: end date − start date |
| Confirmation the visit concludes before reporting back to duty | Checkbox | ✱ | Per Clause C |

**Minimum Notice live countdown banner (gold background, navy text):**
```
📅  You must submit at least 30 calendar days before your visit
    start date — 18 days remaining until this deadline closes
    for your selected dates.
```
If fewer than 30 days remain for the chosen start date, the banner turns red and the Next button is disabled until the date is adjusted.

---

### 5.8 Step D — Research Proposal & Output

**Section heading:** `D. Research Proposal & Output`

| Field | Type | Required | Notes |
|---|---|---|---|
| Purpose of the Visit / Brief Research Proposal | Textarea (800 chars) | ✱ | |
| Intended Output of the Visit | Textarea (400 chars) | ✱ | e.g. publication target, joint grant proposal |
| Updated Research Profile / CV | File upload (PDF) | ✱ | Mirrors the required upload in Section F |

**Intelligent Application Assistant panel (right side, collapsible):**
```
🤖 Application Assistant
━━━━━━━━━━━━━━━━━━━━━━
💡 Suggestion: Faculty in Finance &
Accounting most frequently cite joint
publication or grant-proposal outputs.

📋 Policy Check
[View Clause N Summary — Director of
Research review criteria]
```

---

### 5.9 Step E — Eligibility Checklist

**Section heading:** `E. Eligibility Checklist`
**Caption:** `These checks run automatically and cannot be edited. Any failed condition blocks submission and cites the relevant policy clause.`

Each criterion is rendered as a large status card, auto-computed (no faculty input):

```
┌─ ✅ ─────────────────────────────────────────────────────┐
│  Not on probation                          [📘 Clause H] │
│  ✅ Verified — HR feed confirms active, non-probationary │
│     status as of 11 Jun 2026.                            │
└────────────────────────────────────────────────────────────┘
```

If a check fails:
```
┌─ ❌ ─────────────────────────────────────────────────────┐
│  Departmental 25% cap                      [📘 Clause D] │
│  ❌ Blocked — Finance & Accounting is currently at        │
│     27% participation for this cycle (3 of 11 faculty).   │
│     You may join the waitlist to be notified if a slot    │
│     opens.                                                │
│     [Join Waitlist]                                       │
└────────────────────────────────────────────────────────────┘
```

**Five checks displayed in order:**

| # | Criterion | Clause | Outcome shown |
|---|---|---|---|
| 1 | Not on probation | H | ✅ / ❌ |
| 2 | Not on resignation notice | I | ✅ / ❌ |
| 3 | Departmental 25% cap not exceeded | D | ✅ / ❌ (+ Join Waitlist) |
| 4 | Prior-year publication compliance satisfied (if applicable) | G / J | ✅ / ❌ / Not Applicable |
| 5 | Senior administrative role flag | K | ℹ️ Informational — triggers mandatory VPAA clearance later, does not block |

**First-time applicant priority badge** (shown only if the department is near capacity):
```
⭐ Priority — First-time applicants receive priority consideration
   under Clause J when departments are near their quota.
```

If all blocking checks pass → green banner:
```
✅  All eligibility criteria met. You may proceed to the next step.
```

The "Next" button is disabled until every blocking check shows ✅ (the waitlist option allows the faculty member to still save the application as a waitlisted draft).

---

### 5.10 Step F — Document Uploads

**Section heading:** `F. Document Uploads`

Each upload field is displayed as a card:

```
┌────────────────────────────────────────────────────────────┐
│  📎  Detailed Research Visit Plan                 REQUIRED │
│      Must cover the full duration of the visit.             │
│                                                            │
│  ┌──────────────────────────────────────────┐             │
│  │  Drag & drop your file here, or Browse   │             │
│  │  Accepted: PDF only · Max size: 10MB     │             │
│  └──────────────────────────────────────────┘             │
│                                                            │
│  After upload:                                             │
│  📄  visit_plan_manchester2026.pdf  [✕ Remove]            │
└────────────────────────────────────────────────────────────┘
```

| Document | Required |
|---|---|
| Detailed Research Visit Plan (full duration) | ✱ Required |
| Invitation Letter from Host Institution (signed by Dept. Head/Dean) | ✱ Required |
| Updated Research Profile / CV | ✱ Required — mirrors Step D |
| Collaborator Bio | Conditional — required only if a collaborator is named in Step B |

The Next button is disabled until all required documents for the selected visit type are uploaded.

**Progress note:** Shows "3 of 3 required documents uploaded ✅"

---

### 5.11 Step G — Calendar & Coverage

**Section heading:** `G. Calendar & Coverage`

| Field | Type | Required | Notes |
|---|---|---|---|
| Known College/UD calendar events during the requested period | Textarea (400 chars) | ✱ | e.g. conferences, accreditation visits |
| Teaching/administrative coverage plan during absence | Textarea (400 chars) | ✱ | |

**Declaration checkbox (bottom of step):**
```
☐  I confirm that all information provided in this application
   is accurate and complete. I understand that submitting a
   false or incomplete application may result in rejection
   and disciplinary action.
```
The Submit button on this step is disabled until this checkbox is checked.

---

### 5.12 Submission Confirmation Screen

After clicking "Submit Application":

```
┌─────────────────────────────────────────────────────────────────┐
│                                                                 │
│              ✅  Application Submitted Successfully             │
│                                                                 │
│   Your application has been submitted and assigned:            │
│                                                                 │
│         SRV-2026-CB-0017                                        │
│         [monospace, 20px, --ud-navy, centred]                   │
│                                                                 │
│   Your College Dean has been notified and will review your     │
│   application within 3 working days.                           │
│                                                                 │
│   You will receive email notifications at each stage.          │
│                                                                 │
│   [View Application Status]    [Submit Another Application]    │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

**Waitlisted submission variant** (when Step E quota check resolved as "join waitlist"):
```
⏳  You've Been Added to the Waitlist
    Finance & Accounting is currently at capacity (27%).
    You'll be notified automatically if a slot opens this cycle.
    [View Waitlist Position]
```

---

## 6. Screen 04 — Faculty: Application Status & Detail View

### 6.1 Purpose
Faculty member views the full details of a submitted application and tracks its progress through the four-stage approval chain.

### 6.2 Layout

**Breadcrumb:** `Home  >  My Applications  >  SRV-2026-CB-0017`

**Page title area:**
```
University of Manchester — Manchester, United Kingdom
12–26 July 2026 · Individual Research
[Status badge: Pending Dean]           [SRV-2026-CB-0017 — monospace]
```

**Page-level action bar (top right):**
```
[Download Application PDF]  [ghost button]
```
If status is "Returned": `[Edit & Resubmit]` primary button also appears here.
If status is "Approved": `[Download Approval Letter]` primary button appears, alongside a small QR code thumbnail.

---

**Full page scroll layout — sections top to bottom:**

**Section 1 — Approval Pipeline (prominent, at the top):**

Horizontal stepper spanning full width:
```
  ✅          ⏳           ○           ○           ○
  Dean      Director      VP        President     Done
Approved   In Review    Waiting     Waiting      Waiting
14 Jun     [Current]
```

Below each completed stage:
- Approver name: `Prof. Khalid Al Suwaidi`
- Date & time: `14 Jun 2026, 10:32`
- Comment (if any): shown in a small speech bubble on hover

---

**Section 2 — Application Details (tabbed):**

Three tabs:
- **Application Details** (default active) — read-only render of all 7 form sections (A–G), displayed cleanly, grouped by section
- **Uploaded Documents** — list of uploaded files with name, size, upload date, and a download icon button each
- **Approval Comments Thread** — chronological thread of all approver comments, returns, and Q&A exchanges

**Application Details tab layout:**
Each section (A–G) is a collapsible card:
```
▼  A. Applicant Information                             [Expand / Collapse]
   ──────────────────────────────────────────────────
   Full Name          Dr. Sara Al Bloushi
   Employee ID        UD-FAC-2089
   College            College of Business
   ...
```

**Approval Comments Thread tab layout:**
```
[Dean — College of Business]                          14 Jun 2026, 10:32
  "Approved. Departmental quota confirmed within limits."
  — Prof. Khalid Al Suwaidi, Dean CB

[Director of Research]                                Current Stage
  ⏳ Awaiting review...
```

---

**Section 3 — Post-Visit Obligations (shown only after the visit end date has passed):**

Card:
```
┌──────────────────────────────────────────────────────┐
│  ✅  Post-Visit Obligation Tracker                    │
│  3 obligations · 1 of 3 complete                     │
│  Next due: Progress Report — 5 Aug 2026               │
│  [View Post-Visit Tasks →]                            │
└──────────────────────────────────────────────────────┘
```

---

## 7. Screen 05 — Faculty: Post-Visit Obligation Tracker

### 7.1 Purpose
This is the module faculty members most frequently miss today. Once a visit's end date passes, SRVS automatically activates this tracker, listing the three post-visit obligations with live countdowns and an evidence-upload path for each.

### 7.2 Layout

**Breadcrumb:** `Home  >  Post-Visit Tasks  >  University of Manchester`

**Page title:**
```
Post-Visit Compliance
University of Manchester, UK · Visit ended: 26 July 2026
[Status badge: 1 of 3 obligations complete]
```

**Top alert (if an obligation is overdue):**
```
⚠️  You have 1 overdue obligation. Please complete it as soon as
    possible. Your Dean has been notified.
[Orange banner, full width]
```

**Obligation Cards — stacked vertically, one per requirement:**

Each card:
```
┌── [Status colour left border: red=overdue, teal=in progress, green=complete] ──┐
│                                                                                 │
│  [Status: 🔴 Overdue]                Due: 5 Aug 2026                          │
│                                                                                 │
│  Progress Report                                                                │
│  Submit a written progress report to your Dean, matching the                  │
│  originally submitted visit plan.                                              │
│                                                                                 │
│  [📎 Upload Evidence]              [i] Policy: Section 2, Item 1               │
│                                                                                 │
└─────────────────────────────────────────────────────────────────────────────────┘
```

**Three obligations displayed in order:**

| # | Obligation | Deadline | Evidence |
|---|---|---|---|
| 1 | Submit a written progress report to the Dean | 10 working days after return | File upload |
| 2 | Deliver a research seminar presentation sharing the visit experience and outcomes | Within the current/next academic semester | Confirm seminar date in-system; slide upload optional |
| 3 | Demonstrate progress toward a Scopus-indexed publication (UD + host affiliation) | Within 1 year of return, quarterly checkpoints | Upload proof at each checkpoint (acceptance letter, submission confirmation, DOI) |

**Obligation 2 expands to show an inline scheduling form:**
```
Research Seminar Presentation
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Scheduled Date:     [Date picker]
College Seminar Series:  [Dropdown]
[Optional: Upload Slides]
[Confirm Seminar Date]
```

**Obligation 3 expands to show the quarterly checkpoint timeline:**
```
Publication Progress — 12-Month Timeline
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
●───────●───────●───────●───────🏁
Return  3 mo    6 mo    9 mo    12 mo
        ✓ Done  ✓ Done  ⏳ Due   Final
[Upload Checkpoint Evidence]
```
At the 11-month mark, the card turns amber with a "Final Notice" tag; if month 12 passes with no compliant evidence, the card turns permanently red and displays:
```
🔴  Marked Publication Non-Compliant
    This blocks eligibility for a new Short Research Visit
    application next cycle (Clauses G, J) until resolved.
```

**Bottom — completion summary:**
```
[Progress bar showing 1/3 complete — gold fill]
All obligations must be completed within their stated deadlines to
remain eligible for future Short Research Visit applications.
```

---

## 8. Screen 06 — Approver: Home Dashboard (Dean · Director of Research · VPAA · President)

### 8.1 Purpose
Primary landing screen for all four approver roles. Shows pending queue, quota snapshot, and quick actions. Layout adapts slightly per role (e.g. Dean sees only their college; Director of Research, VPAA, and President see university-wide data).

### 8.2 Layout

**Welcome bar:**
```
Good morning, Prof. Khalid Al Suwaidi
Dean — College of Business
                                    [Go to Pending Approvals →] [primary button]
```

**KPI Cards row (4 cards):**
| Card 1 | Card 2 | Card 3 | Card 4 |
|---|---|---|---|
| Pending My Approval | Approved This Cycle | Rejected This Cycle | Avg. Decision Time |
| [Count — gold if > 0] | [Count] | [Count] | [X days] |

**Overdue alert (if applicable):**
```
🔴  2 applications are overdue for your review.
    Escalation notices have been sent to your office.
    [Review Now →]
[Red banner, full width]
```

**Departmental Quota Snapshot card (Dean view shows own college; other roles show a university-wide mini heat map):**
```
┌──────────────────────────────────────────┐
│  🗺️  Departmental Quota — College of Business │
│  Finance & Accounting     ████████░░ 27% 🔴│
│  Marketing                ███░░░░░░░ 9%  🟢│
│  Management                █████░░░░ 18% 🟡│
│  [View Full Heat Map →]                   │
└──────────────────────────────────────────┘
```

**Main table — Pending Approvals (top 10, with "View all" link):**

Table columns — same as full Pending Approvals Queue (Section 9), showing top 10 by SLA urgency.

**Bottom row — two columns:**

**Left: Recent Decisions (last 5 actions I took):**
```
Section heading: My Recent Decisions
[Table: Reference · Faculty · Host Institution · Decision · Date · Comments snippet]
```

**Right: Quick Stats chart:**
```
Section heading: This Cycle
[Small donut chart: Approved vs Rejected vs Pending — UD colours]
[Below chart: total applications this cycle from my college/all]
```

---

## 9. Screen 07 — Approver: Pending Approvals Queue

### 9.1 Purpose
Full list of applications currently awaiting the logged-in approver's action. Primary workhorse screen for approvers.

### 9.2 Layout

**Page title:** `Pending Approvals`
**Caption:** `Applications currently awaiting your review and decision.`

**Top action bar:**
```
[Global search bar — "Search by name, host institution, reference..."]
[Filter: College ▾] [Filter: Status ▾] [Filter: Date Range ▾]  [Clear filters]
                                        Showing 9 applications  [Table / Card ▾]
```

**View toggle (top right):**
- **Table view** (default) — standard table layout
- **Card view** — each application shown as a horizontal card, groupable by status

**Table view columns:**

| # | Reference | Faculty Name | College/Dept | Host Institution | Country | Submitted | Days Waiting | SLA | Status | Action |
|---|---|---|---|---|---|---|---|---|---|---|
| 1 | SRV-2026-CB-0017 | Dr. Sara Al Bloushi | CB / Finance & Accounting | Univ. of Manchester | UK | 12 Jun | 2d | 🟡 | [Pending Dean] | Review |

**SLA column:**
- 🟢 Green dot: within SLA (< 50% elapsed)
- 🟡 Amber dot: approaching SLA (50–99% elapsed), shows tooltip with hours remaining
- 🔴 Red dot: overdue, row has red left border

**Card view — each card:**
```
┌─────────────────────────────────────────────────────────────────┐
│  SRV-2026-CB-0017                            [Pending Dean] 🟡  │
│  Dr. Sara Al Bloushi · College of Business, Finance & Accounting │
│  University of Manchester — Manchester, UK · 12–26 Jul 2026     │
│  Submitted: 12 Jun 2026 · Waiting: 2 days · ⭐ First-time        │
│                          [Review Application]  [Quick Approve]  │
└─────────────────────────────────────────────────────────────────┘
```

**Quick Approve** — opens a small modal without leaving the queue:
```
┌─────────────────────────────────────┐
│  Quick Decision                     │
│  SRV-2026-CB-0017                   │
│  Dr. Sara Al Bloushi — Univ. of Manchester │
│                                     │
│  Comment (optional):                │
│  [Textarea]                         │
│                                     │
│  [✅ Approve]  [⚠️ Return]  [❌ Reject] │
└─────────────────────────────────────┘
```

---

## 10. Screen 08 — Approver: Single Application Review

### 10.1 Purpose
Full review screen for a single application. Approver reads all details and takes an action. A fixed action bar at the bottom is always visible. The Director of Research stage additionally surfaces the Clause N research-quality criteria checklist.

### 10.2 Layout

**Breadcrumb:** `Home  >  Pending Approvals  >  SRV-2026-CB-0017`

**Page title area:**
```
University of Manchester — Manchester, United Kingdom
Dr. Sara Al Bloushi · College of Business, Finance & Accounting
[Status: Pending Your Approval]              [SRV-2026-CB-0017 — monospace]
```

---

**Full page scroll — sections:**

**Section 1 — Approval Pipeline** (same horizontal stepper as Faculty view, Section 6)
Current stage is highlighted. Previous approvers' names and dates are shown.

**Section 2 — Application Summary strip:**
Quick-read horizontal strip with key facts:
```
📍 Manchester, UK  ·  📅 12–26 Jul 2026  ·  🤝 Individual Research
✅ Top 200 — Preferred  ·  🗺️ Dept. Quota: 27% 🔴  ·  ⭐ First-time applicant
```

**Section 3 — Tabbed Detail (3 tabs):**
Same three tabs as faculty view (Application Details / Documents / Approval History). See Section 6.2.

Documents tab: Files are downloadable via icon buttons. Approvers cannot delete or replace documents.

**Section 4 — Director of Research Only: Clause N Criteria Checklist**

Shown only when the current stage is "Pending Director of Research":
```
Research Quality Assessment — Clause N Criteria
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
☐  Research project quality / UD priority fit
☐  Faculty research record
☐  Publication potential
☐  Host institution suitability
☐  Potential benefit to UD
☐  Long-term collaboration potential

[Optional notes per criterion — expandable text field]
```
All six boxes must be checked before the Approve button activates at this stage.

**Section 5 — VPAA Only: Administrative Responsibility Clearance**

Shown only when the Senior Administrator flag is set on the applicant's profile:
```
⚠️  Administrative Responsibility Clearance Required (Clause K)
☐  I confirm that appropriate administrative coverage has been
   arranged for this faculty member's senior role during the
   visit period.
```
The Approve button is disabled at the VPAA stage until this box is checked.

**Section 6 — Previous Approver Comments (always visible, not in tab):**
Below the tabs, always visible:
```
Comments from Previous Approvers
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[Dean · Prof. Khalid Al Suwaidi · 14 Jun 2026, 10:32]
"Approved. Departmental quota confirmed within limits."
```

---

**Fixed bottom action bar (always visible, sticky at bottom of viewport):**

```
┌────────────────────────────────────────────────────────────────────────────────┐
│                                                                                │
│  Add a comment (required if Returning or Rejecting):      [Character: 0/500]  │
│  ┌────────────────────────────────────────────────────────────────────────┐   │
│  │  Type your comments, instructions, or reason here...                  │   │
│  └────────────────────────────────────────────────────────────────────────┘   │
│                                                                                │
│  [← Back to Queue]   [Request Information]   [⚠️ Return]  [❌ Reject]  [✅ Approve] │
│                                                                                │
└────────────────────────────────────────────────────────────────────────────────┘
```

**Button behaviours:**
- **Approve:** Opens confirmation modal → "Confirm Approval — This will advance the application to the Director of Research." [Confirm] [Cancel]. On confirm: digital signature captured (timestamp + name), application moves to next stage, notifications sent.
- **Return:** Comment is required. Modal: "Return to Faculty — The faculty member will be notified to revise and resubmit." [Confirm Return] [Cancel]
- **Reject:** Comment is required. Modal (red): "Reject Application — This action is final. The application will be archived and the faculty member notified." [Confirm Rejection] [Cancel]
- **Request Information:** Opens an information request thread where the approver types a question. The faculty member is notified and responds in-system. The thread appears in the Approval History tab.
- **Final stage (President):** "Approve" is replaced with `[✅ Final Approve]`. Confirming triggers digital signature capture and auto-generation of the official approval letter (with embedded QR code).

---

## 11. Screen 09 — Approver: All Applications View

### 11.1 Purpose
Full searchable, filterable view of all applications within the approver's scope (college-filtered for Dean, university-wide for Director of Research, VPAA, and President).

### 11.2 Layout

**Page title:** `All Applications`
**Caption (Dean view):** `Showing all applications from College of Business`

**Top — KPI summary strip (above the table):**
```
[Total: 38]  [Approved: 22]  [Pending: 9]  [Rejected: 4]  [Waitlisted: 3]
```
Each number is a clickable filter — clicking "Pending: 9" filters the table to show only pending.
Cycle selector on the right: `Summer 2026 ▾`

**View toggle:** Table / Card view toggle (top right), same as Pending Approvals Queue.

**Full table — all applications:**

Columns: Reference · Faculty Name · College/Dept · Host Institution · Country · Start Date · Submitted Date · Final Status · Action

All table standards apply (search, sort, filter, pagination, row click).

**Status filter dropdown options:** All · Draft · Pending Dean · Pending Director · Pending VPAA · Pending President · Approved · Rejected · Returned · Waitlisted

---

## 12. Screen 10 — Departmental Quota Heat Map

### 12.1 Purpose
A visual, real-time view of every department's participation against the 25% cap, including a predictive warning if pending (not-yet-approved) applications would push a department over the line. Available to Dean (own college), Director of Research and Executive roles (university-wide).

### 12.2 Layout

**Page title:** `Departmental Quota Heat Map`
**Caption:** `Live participation against the 25% departmental cap (Clause D).`

**Top — filter bar:**
```
[Filter: College ▾]   [Cycle: Summer 2026 ▾]   [Toggle: Include Pending Applications]
```

**Heat map grid — one tile per department:**

```
┌───────────────────────────┐  ┌───────────────────────────┐  ┌───────────────────────────┐
│  Finance & Accounting     │  │  Marketing                │  │  Management               │
│  ████████████░░░░░  27%   │  │  ███░░░░░░░░░░░░░░  9%    │  │  █████░░░░░░░░░░░  18%    │
│  3 of 11 faculty active   │  │  1 of 11 faculty active   │  │  2 of 11 faculty active   │
│  🔴 At Cap — Blocked       │  │  🟢 Healthy                │  │  🟡 Approaching Cap        │
│  ⚠️ +1 pending would →30% │  │                            │  │  ⚠️ +1 pending would →27% │
└───────────────────────────┘  └───────────────────────────┘  └───────────────────────────┘
```

- Tile background tint follows the heat-map colour scale in Section 1.1
- The "⚠️ +N pending would →X%" line only appears when "Include Pending Applications" is toggled on, and is the predictive warning required by FR-ELIG-001
- Clicking a tile opens a drawer listing the named faculty members currently counted in that department's percentage, with visit dates

**Below the grid — University-wide summary table (Director of Research / Executive views only):**

| College | Department | Headcount | Active on Visit | % of Cap | Status |
|---|---|---|---|---|---|
| Business | Finance & Accounting | 11 | 3 | 27% | 🔴 At Cap |
| Business | Marketing | 11 | 1 | 9% | 🟢 Healthy |
| Business | Management | 11 | 2 | 18% | 🟡 Approaching |

**Waitlist panel (right side, collapsible):**
```
⏳ Waitlist — Finance & Accounting
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
1. Dr. Omar Khalil — joined 10 Jun 2026
2. Dr. Fatima Rashed — joined 13 Jun 2026

If a slot opens, the next faculty member is
notified automatically and given 48 hours to
confirm before the slot passes to the next
in line.
```

---

## 13. Screen 11 — Post-Visit Compliance Dashboard

### 13.1 Purpose
Deans and the Director of Research see a consolidated view of every returned faculty member's obligation status, so nobody has to remember to chase a report, a seminar date, or publication evidence manually.

### 13.2 Layout

**Page title:** `Post-Visit Compliance Dashboard`
**Caption:** `Who owes what, and by when.`

**KPI Cards row (4 cards):**
| Card 1 | Card 2 | Card 3 | Card 4 |
|---|---|---|---|
| Faculty Currently Tracked | 🟢 Complete | 🟡 In Progress | 🔴 Overdue |
| [Count] | [Count] | [Count] | [Count — red if > 0] |

**Main table — Compliance Status by Faculty:**

| Faculty Name | College/Dept | Host Institution | Returned | Progress Report | Seminar | Publication | Overall |
|---|---|---|---|---|---|---|---|
| Dr. Sara Al Bloushi | CB / Finance & Accounting | Univ. of Manchester | 26 Jul 2026 | 🔴 Overdue | 🟡 Not yet due | 🟡 Checkpoint 1 of 4 | 🔴 |

- Each obligation column shows the coloured status dot from Section 1.1, with a tooltip giving the exact due date
- "Overall" column shows the worst status among the three obligations
- Clicking a row opens a read-only view of that faculty member's full Post-Visit Obligation Tracker (Section 7), with an option to send a manual reminder

**Escalation banner (if any faculty member crosses an escalation threshold):**
```
🔴  2 faculty members have overdue obligations requiring escalation.
    [View Escalated Cases →]
```

**Filter bar:**
```
[Filter: College ▾]  [Filter: Obligation Type ▾]  [Filter: Status ▾]  [Export to Excel]
```

---

## 14. Screen 12 — Executive Dashboard (VPAA & President)

### 14.1 Purpose
High-level real-time view of the entire Short Research Visits ecosystem. Designed for VP of Academic Affairs and the University President. Data-dense but visually clear, and directly useful for accreditation reporting.

### 14.2 Layout

**Page title:** `Executive Dashboard`
**Right side:** `Cycle: Summer 2026 ▾` · `[Export PDF Report]` [ghost button] · `[Last updated: 2 mins ago]` (caption)

---

**Row 1 — KPI Counter Cards (5 cards, equal width):**

Each card:
- White, gold top border `3px`, `16px` padding
- Large number (`36px`, bold, `--ud-navy`)
- Label below (`13px`, `--ud-text-mid`)
- Trend indicator: small up/down arrow with % vs. last cycle (`12px`, green/red)

| Card 1 | Card 2 | Card 3 | Card 4 | Card 5 |
|---|---|---|---|---|
| Total Applications | Approved | Pending | Rejected | Waitlisted |
| YTD count | YTD count | In workflow | YTD count | Currently queued |
| ↑ 14% vs last cycle | ↑ 9% | — | ↓ 2% | ↑ 1 |

---

**Row 2 — Two charts, side by side:**

**Left chart (60%) — Applications by Month (bar chart):**
- X-axis: months across the academic year
- Y-axis: count
- Bars: navy for approved, gold for pending, red for rejected, stacked
- Hover tooltip: exact counts per status per month

**Right chart (40%) — Host Institutions by Ranking Tier (donut chart):**
- Segments: QS/THE/ARWU Top 200 vs. Other
- Centre: total count
- Legend below with count and percentage per tier

---

**Row 3 — Three columns:**

**Column 1 (33%) — Approval Cycle Time:**
Line chart — average days per stage across the current cycle.
```
Avg. Days per Stage — Summer 2026
[Line chart: Dean · Director · VPAA · President on X-axis, days on Y-axis]
```
Annotation: Any stage > SLA target is highlighted in red.

**Column 2 (33%) — Departmental Quota Heat Map (compact view):**
Mini version of Screen 10's grid, with `[View Full Heat Map →]` link.

**Column 3 (33%) — Publication Compliance Tracker:**
```
One-Year Publication Compliance — Prior Cycle
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[Semi-circular gauge — gold arc fill, navy arc remaining]
82% compliant
9 of 11 faculty submitted qualifying evidence
within 12 months of return.
```

---

**Row 4 — College Comparison Table:**

```
College Comparison — Summer 2026
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

| College | Applications | Approved | Rejected | Waitlisted | Avg. Cycle Days | Publication Compliance |
|---|---|---|---|---|---|---|
| Business | 38 | 22 | 4 | 3 | 8.4 | 82% |
| Engineering & IT | 26 | 19 | 2 | 1 | 7.1 | 88% |
| Law | 11 | 8 | 1 | 0 | 9.0 | 75% |
| **Total** | **75** | **49** | **7** | **4** | **8.1** | **82%** |

---

**Row 5 — Research Mobility & Output Tracker (Director of Research + VPAA + President):**

```
Host Institutions by Ranking Tier — Year-on-Year
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[Bar chart: year-on-year comparison, current cycle vs last 3 cycles]
[Below: Table — Top 10 Host Institutions by Faculty Count]
```

**Annual Report shortcut card:**
```
📄  University of Dubai Short Research Visits Annual Report
    Auto-generated at the end of each academic year — visits by
    college, host institutions and ranking tiers, and publication
    compliance rates. Directly usable for accreditation submissions.
    [Generate Report Now]  [View Last Year's Report]
```

---

## 15. Screen 13 — HR: Home & Eligibility Feed

### 15.1 Purpose
HR has no approval authority in SRVS — its role is purely as a data source for the eligibility engine and an observer of approved visit leave. This screen shows the nightly sync status and a read-only feed; raw probation/resignation data is never surfaced to any other role.

### 15.2 Layout

**Page title:** `Eligibility Feed Status`
**Caption:** `Read-only view. This data powers the automated eligibility checks faculty see when applying.`

**Top — Sync status card:**
```
┌─────────────────────────────────────────────────────────────┐
│  🔄  HRIS Sync Status                                        │
│  Last successful sync: Today, 02:00 AM        ✅ Healthy    │
│  Records synced: 412 faculty profiles                       │
│  [Run Manual Sync Now]  [secondary button]                   │
└─────────────────────────────────────────────────────────────┘
```
If the sync fails or is stale (> 24 hours), the card turns red with: "⚠️ Sync overdue — eligibility checks may be using outdated data."

**Main table — Active Visit Leave (read-only):**
| Faculty Name | College/Dept | Host Institution | Country | Leave Start | Leave End | Approved By |
|---|---|---|---|---|---|---|
| Dr. Sara Al Bloushi | CB / Finance & Accounting | Univ. of Manchester | UK | 12 Jul 2026 | 26 Jul 2026 | University President |

- All rows are read-only. No action buttons.
- Export to Excel available (top right).

**Eligibility Exceptions panel (visible only to System Administrator alongside HR, per FR-ELIG-002):**
```
Logged Manual Overrides
━━━━━━━━━━━━━━━━━━━━━━
Dr. Omar Khalil — probation override logged 9 Jun 2026
by System Administrator. Reason: documented exception
approved by HR Director (ref. memo HR-2026-014).
```

**Faculty Directory tab:**
Simple searchable read-only list of all faculty members with their college/department and current visit-leave status. No probation or resignation status is ever displayed in this directory — only a computed "Eligible / Not Currently Eligible" badge.

---

## 16. Screen 14 — System Admin: Home & User Management

### 16.1 Purpose
System Administrator manages all users, roles, and access across the platform.

### 16.2 Layout — Admin Home

**Page title:** `System Administration`

**KPI Cards (4):**
| Total Active Users | New This Month | Pending Role Assignment | System Alerts |
|---|---|---|---|
| [Count] | [Count] | [Count — gold if > 0] | [Count — red if > 0] |

**Quick links grid (2×3):**
Large icon cards linking to each admin section:
- User Management · Department Headcounts · Workflow Config · Audit Log · Academic Year · Notification Templates

### 16.3 Layout — User Management

**Page title:** `User Management`

**Top action bar:**
```
[Search users...] [Filter: Role ▾] [Filter: College ▾] [Filter: Status ▾]
                                                        [+ Add New User]  [primary button]
```

**User table:**
| Name | Employee ID | Email | Role | College/Dept | Status | Last Login | Actions |
|---|---|---|---|---|---|---|---|
| Dr. Sara Al Bloushi | UD-FAC-2089 | salbloushi@ud.ac.ae | Faculty | CB / Finance & Accounting | Active | 16 Jun 2026 | Edit · Deactivate |

**Edit User panel (opens as a right-side drawer, `400px` wide):**
```
Edit User
━━━━━━━━━━━━━━━━━━━━━━━━━
Full Name:      [Text input — read from AD, editable]
Employee ID:    [Read-only]
Email:          [Read-only — from AD]
Role:           [Dropdown: all roles]
College/Dept:   [Dropdown — if applicable]
Senior Administrator flag: [Toggle — drives Clause K VPAA clearance]
Status:         [Toggle: Active / Inactive]

Delegation Settings:
Auto-delegate after: [Number] hours to [User search]

[Save Changes]  [Cancel]
```

---

## 17. Screen 15 — System Admin: Department Headcounts & Quota Configuration

### 17.1 Purpose
Admin maintains the per-department faculty headcounts that feed the quota engine's 25% cap calculation — the single source of truth Deans and faculty rely on.

### 17.2 Layout

**Page title:** `Department Headcounts & Quota Configuration`
**Caption:** `These figures directly determine each department's 25% participation cap.`

**Top action bar:**
```
[Search departments...] [Filter: College ▾]            [+ Add Department]  [primary button]
```

**Department table:**
| College | Department | Total Headcount | Active on Visit | Current % | Last Updated | Action |
|---|---|---|---|---|---|---|
| Business | Finance & Accounting | 11 | 3 | 27% 🔴 | 1 Sep 2025 | Edit |

**Edit Department drawer:**
```
Edit Department
━━━━━━━━━━━━━━━━━━━━━━━━━
Department Name:        [Text input]
College:                 [Dropdown]
Total Faculty Headcount: [Number input]
Director of Research:    [User search]

[i] Changing headcount recalculates the live quota
    percentage immediately for this cycle.

[Save Changes]  [Cancel]
```

**Audit note (bottom of page):**
```
[i] All headcount changes are logged in the Audit Log with the
    old value, new value, and the admin who made the change.
```

---

## 18. Screen 16 — System Admin: Workflow & Notification Configuration

### 18.1 Purpose
Admin configures SLA thresholds, the approval chain structure, draft/reminder windows, and email notification templates.

### 18.2 Layout

**Page title:** `Workflow & Notification Configuration`

**Two tabs:**

**Tab 1 — SLA & Approval Settings:**

```
Research Visit Approval Chain — SLA Thresholds
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[Editable table]
```
| Stage | Approver | SLA (working days) | Escalation Recipient | Edit |
|---|---|---|---|---|
| 1 | Dean | 3 | Director of Research | ✏️ |
| 2 | Director of Research | 3 | VP Academic Affairs | ✏️ |
| 3 | VP Academic Affairs | 2 | University President | ✏️ |
| 4 | University President | 2 | — | ✏️ |

**Other configurable thresholds:**
- **Minimum notice window:** `[Number] days` (default: 30, Clause L)
- **Draft retention period:** `[Number] days` (default: 90)
- **Departmental cap percentage:** `[Number] %` (default: 25, Clause D)
- **Progress report deadline:** `[Number] working days post-return` (default: 10)
- **Publication compliance window:** `[Number] months` (default: 12)

**Tab 2 — Notification Templates:**

List of all notification types (e.g. "Application Submitted", "Approver Action Required", "Quota Cap Reached", "Waitlist Slot Opened", "Post-Visit Obligation Due", "Publication Non-Compliant").

Clicking a template opens an editor:
```
Template: Quota Cap Reached — Faculty Notification
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Subject: [Text input — supports {{variables}}]
Body:    [Rich text editor]
         Available variables: {{applicant_name}}, {{reference}},
         {{department_name}}, {{current_percentage}}, {{deep_link}}
[Preview] [Save Template]
```

---

## 19. Screen 17 — System Admin: Audit Log

### 19.1 Purpose
Immutable, searchable record of all system events for compliance and security review.

### 19.2 Layout

**Page title:** `Audit Log`
**Caption:** `Immutable record of all system events. Retained for 7 years.`

**Top filter bar:**
```
[Search by user, action, entity...] [Date Range picker] [Filter: Action Type ▾] [Filter: Role ▾]
                                                                            [Export CSV] [Export PDF]
```

**Audit log table:**
| Timestamp | User | Role | Action | Entity Type | Entity Reference | IP Address | Details |
|---|---|---|---|---|---|---|---|
| 12 Jun 2026 09:14:02 | Dr. Sara Al Bloushi | Faculty | SUBMITTED | Application | SRV-2026-CB-0017 | 10.0.2.18 | View |

"View" opens a detail modal showing old value vs. new value (JSON diff for changed records, e.g. headcount edits or manual eligibility overrides).

No edit or delete actions — this table is read-only by design.

---

## 20. Screen 18 — System Admin: Academic Year & Summer Session Management

### 20.1 Purpose
Admin opens and closes academic year / summer session cycles and manages historical data archiving.

### 20.2 Layout

**Page title:** `Academic Year & Summer Session Management`

**Current cycle card:**
```
┌─────────────────────────────────────────────────────────────┐
│  CURRENT SUMMER SESSION CYCLE                                │
│  Summer 2026                              Status: 🟢 Active  │
│  Applications: 75 total                                      │
│  Session window: 1 July 2026 – 31 August 2026                 │
│  Opened for applications: 15 April 2026                       │
│                                                                │
│  [Close Cycle]  [danger button]                               │
└─────────────────────────────────────────────────────────────┘
```

Closing the cycle triggers a confirmation modal explaining consequences (no new submissions, data archived as read-only, post-visit obligations for that cycle continue tracking independently).

**[+ Open New Cycle]** button — opens setup wizard:
1. Set cycle label (e.g. Summer 2027)
2. Set summer session start/end dates
3. Confirm department headcounts carry over (or re-import from HRIS)
4. Confirm SLA settings carry over
5. Activate

**Previous cycles table:**
| Cycle | Applications | Approved | Waitlisted | Status | Action |
|---|---|---|---|---|---|
| Summer 2025 | 63 | 47 | 2 | Closed | View Archive |

---

## 21. Screen 19 — Notifications Centre (All Roles)

### 21.1 Purpose
Full notifications page accessible to all roles. Shows complete history of all notifications, grouped and filterable.

### 21.2 Layout

**Page title:** `Notifications`

**Top action bar:**
```
[Filter: All ▾ / Unread / Read]   [Filter: Type ▾]      [Mark all as read]
```

**Notifications list — grouped by date:**

```
TODAY — 16 June 2026
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[● Unread] 🔔 Application Approved by Dean                      10:32
            SRV-2026-CB-0017 has been approved by Prof. Khalid
            Al Suwaidi and advanced to the Director of Research.
            [View Application →]

[● Unread] ⚠️  Post-Visit Obligation Overdue                    09:00
            Progress Report for University of Manchester is
            overdue (due: 5 Aug 2026).
            [Complete Now →]

YESTERDAY — 15 June 2026
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[Read]    ✅ Application Fully Approved                         14:15
            SRV-2026-CEIT-0009 has been approved by the
            UD President. Approval letter is now available.
            [View Approval Letter →]
```

Each notification:
- Left: unread indicator dot (gold) or empty (read)
- Icon indicating type
- Title (bold), body (2 lines), reference link
- Right: timestamp
- Full row is clickable — marks as read and navigates to context

---

## 22. Screen 20 — Profile, Settings & Delegation (All Roles)

### 22.1 Purpose
User views and updates their personal profile, notification preferences, and (for approver roles) delegation settings — particularly relevant for SRVS since summer-visit approvals often land while Deans and Directors are themselves partly on leave.

### 22.2 Layout

**Page title:** `My Profile`

**Three tabs:**

**Tab 1 — Profile Information:**
```
[Avatar — circular, 80px]  [Change Photo]

Full Name:         Dr. Sara Al Bloushi    [Read-only — from AD]
Employee ID:       UD-FAC-2089            [Read-only]
Email:              salbloushi@ud.ac.ae    [Read-only]
College/Dept:        CB / Finance & Accounting  [Read-only]
Academic Rank:       Associate Professor    [Read-only]

Editable fields:
Specialisation:    [Text input]
ORCID ID:          [Text input, validated format]
Google Scholar:    [URL input]

[Save Changes]
```

**Note at bottom:** "To update read-only fields, please contact HR or the System Administrator."

**Tab 2 — Notification Preferences:**
Table of notification types with toggles (Email / In-App / Both / Off):
| Notification Type | Email | In-App |
|---|---|---|
| Application status changed | ✅ | ✅ |
| Approver comment received | ✅ | ✅ |
| Post-visit obligation due | ✅ | ✅ |
| Quota / waitlist update | ✅ | ✅ |
| SLA reminder (approvers only) | ✅ | ✅ |

**Tab 3 — Delegation Settings (Approver roles only):**
```
Out-of-Office Delegation
━━━━━━━━━━━━━━━━━━━━━━━━
Auto-delegate pending approvals to:
[User search input — search by name or employee ID]

Delegate after:  [Number] hours without action

Active from:  [Date picker]   to:  [Date picker]
              (leave blank for indefinite)

[Save Delegation Settings]

Current Delegation:
Delegating to: Dr. Layla Hassan
Active: 1 Jul – 15 Jul 2026
[Cancel Delegation]
```
Annotation: This screen directly implements the "Smart Delegation" capability — approvers can set "If I do not act within 48 hours, automatically delegate to [named deputy]," which is especially relevant given that summer-visit approvals often land while approvers themselves are partially on leave.

---

## 23. Component Library Reference

Summary of all reusable components defined in this specification.

### 23.1 Navigation Components
- `<TopHeader>` — global header bar (Section 2.2)
- `<LeftSidebar>` — role-aware sidebar, expanded/collapsed states (Section 2.3)
- `<Breadcrumb>` — page location trail, used on all inner pages
- `<NotificationDropdown>` — bell icon dropdown (Section 2.5)

### 23.2 Data Display Components
- `<KPICard>` — counter card with label, trend indicator, icon (Section 4.2)
- `<StatusBadge>` — coloured status pill (Section 1.8)
- `<PolicyClauseTag>` — clickable clause citation chip (Section 1.9)
- `<DataTable>` — full-featured table with search, sort, filter, pagination (Section 1.6)
- `<ApprovalStepper>` — horizontal pipeline tracker (Section 6.2)
- `<CommentThread>` — chronological approver comments (Section 6.2)
- `<NotificationItem>` — individual notification row (Section 21.2)
- `<HeatMapTile>` — departmental quota tile with predictive warning (Section 12.2)

### 23.3 Form Components
- `<FormSection>` — labelled collapsible section wrapper
- `<AutoFilledField>` — read-only field with blue tint + padlock icon
- `<SystemVerifiedField>` — locked eligibility field with "🔒 System-verified" tag (Section 1.5)
- `<FileUploadCard>` — drag-drop upload area with post-upload file name display
- `<RankingVerificationWidget>` — QS/THE/ARWU live check with badge (Section 5.6)
- `<EligibilityCard>` — auto-computed pass/fail card with clause citation (Section 5.9)
- `<AIAssistantPanel>` — collapsible right-side AI helper (Section 5.8)

### 23.4 Action Components
- `<ActionBar>` — sticky bottom bar with approve/return/reject buttons (Section 10.2)
- `<QuickApproveModal>` — compact in-queue decision modal (Section 9.2)
- `<ConfirmationModal>` — used for all destructive or irreversible actions
- `<EmptyState>` — icon + message + optional CTA (Section 1.7)
- `<AlertBanner>` — full-width contextual alert (red/amber/gold/green)
- `<WaitlistJoinAction>` — inline waitlist join control on a blocked eligibility card (Section 5.9)

### 23.5 Dashboard Components
- `<BarChart>` — applications by month (Section 14.2)
- `<DonutChart>` — host institutions by ranking tier (Section 14.2)
- `<LineChart>` — approval cycle time trend (Section 14.2)
- `<GaugeChart>` — publication compliance percentage (Section 14.2)
- `<RankedList>` — top host institutions by faculty count (Section 14.2)
- `<CollegeComparisonTable>` — multi-college data table (Section 14.2)

### 23.6 Task & Compliance Components
- `<TaskCard>` — post-visit obligation card with status, due date, upload (Section 7.2)
- `<CheckpointTimeline>` — quarterly publication-progress timeline (Section 7.2)
- `<ComplianceStatusRow>` — per-faculty compliance row across all obligations (Section 13.2)
- `<DelegationPanel>` — out-of-office auto-delegation configuration (Section 22.2)

---

## 24. Role-to-Screen Access Matrix

| Screen | Faculty | Dean | Director | VPAA | President | HR | Admin |
|---|---|---|---|---|---|---|---|
| 01 Login | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| 02 Faculty Home | ✅ | — | — | — | — | — | — |
| 03 New Application Form | ✅ | — | — | — | — | — | — |
| 04 Application Status/Detail | ✅ (own) | ✅ | ✅ | ✅ | ✅ | — | ✅ |
| 05 Post-Visit Obligation Tracker | ✅ (own) | — | — | — | — | — | — |
| 06 Approver Home | — | ✅ | ✅ | ✅ | ✅ | — | — |
| 07 Pending Approvals Queue | — | ✅ | ✅ | ✅ | ✅ | — | — |
| 08 Single Application Review | — | ✅ | ✅ | ✅ | ✅ | — | — |
| 09 All Applications View | — | ✅ (college) | ✅ | ✅ | ✅ | — | ✅ |
| 10 Departmental Quota Heat Map | — | ✅ (college) | ✅ | ✅ | ✅ | — | ✅ |
| 11 Post-Visit Compliance Dashboard | — | ✅ (college) | ✅ | — | — | — | ✅ |
| 12 Executive Dashboard | — | — | ✅ | ✅ | ✅ | — | ✅ |
| 13 HR Home & Eligibility Feed | — | — | — | — | — | ✅ | ✅ |
| 14 Admin: User Management | — | — | — | — | — | — | ✅ |
| 15 Admin: Department Headcounts | — | — | — | — | — | — | ✅ |
| 16 Admin: Workflow Config | — | — | — | — | — | — | ✅ |
| 17 Admin: Audit Log | — | — | — | — | — | — | ✅ |
| 18 Admin: Academic Year Mgmt | — | — | — | — | — | — | ✅ |
| 19 Notifications Centre | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| 20 Profile, Settings & Delegation | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |

---

<div align="center">

**University of Dubai · Short Research Visits System**
**Screen Layout & Design Specification · v1.0**

*Confidential — Internal Use Only*

</div>
