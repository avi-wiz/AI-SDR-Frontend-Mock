# WizSDR Sales Agents — Prototype

## What this is

A full end-to-end interactive prototype of **WizSDR** (WizCommerce Sales Agents), a play engine that runs autonomous email sequences for wholesale B2B sales teams. The prototype covers 25 screens across three personas: Sales Rep, Admin, and Simulator.

**Entry point:** `WizSDR Prototype.html` — persona router with tabs at the top.

## Product name

The product is called **WizSDR** (not WizCRM). The parent brand is WizCommerce.

## Design system

Uses the **WizCommerce Design System (Remix)** at `_ds/wizcommerce-design-system-remix-019df7db-e0c4-715b-add3-bb30e9d8a2f2/`. Key rules:
- Square corners everywhere (radius: 0). Pills only for circles (avatars, dots).
- Wiz Orange (#FE7630) used sparingly — one accent per region, never as background for body text.
- Hairlines (1px borders) do structural work, not cards or shadows.
- Typography: Recife (display, weight 300 only), General Sans (UI + all numerals), Geist Mono (identifiers + eyebrows only).
- Numbers always use `.t-num` recipe: General Sans Medium 500, `letter-spacing: -0.01em`, tabular figures.
- No semantic colors (no green/red/amber). Status communicated through copy and hierarchy.
- Type on orange is always black (ink-900).

## Architecture

```
WizSDR Prototype.html          ← Persona router (loads DC files in iframe)
├── WizCRM Sales Agents.dc.html  ← Rep screens (Design Component)
├── WizSDR Admin.dc.html          ← Admin screens (Design Component)
├── WizSDR Simulator.dc.html      ← Simulator screens (Design Component)
├── assets/
│   ├── wiz-logo-white.png        ← Inverse logo for dark header
│   └── wiz-mark-white.svg        ← Mark for dark header
├── uploads/PRD.md                ← Source PRD (full spec)
└── _ds/...                       ← Design system (tokens, fonts, bundle)
```

Each `.dc.html` file is a Design Component — a single self-contained file with an HTML template and a JS logic class. They render directly in a browser with `support.js`.

## Screen map

### Rep screens (`WizCRM Sales Agents.dc.html`)

| ID | Screen | Nav key | What it does |
|----|--------|---------|-------------|
| R1 | Home (My Day) | `home` | Agent summary cards, drafts waiting, handoffs, activity feed with "Why?" links |
| R2 | Agent Inbox | `inbox` | Split-pane email client: draft list + full email preview. Approve/Edit/Reject with feedback. Keyboard hints (A/E/R/S). Filter tabs. |
| R3 | Handoffs | `handoffs` | Buyer reply thread + pre-drafted response. Pre-built cart/quote link chips. Contact update form for "wrong person". Send/Dismiss flow. |
| R4 | Accounts List | `accounts` | 12 accounts table with search, filters, sort. Status badges. Click → R5. |
| R5 | Account Detail | `accounts` (viewingAccount set) | Header stats, Pause/Kill/Manual controls, active play link → R9, agent timeline with expandable "Why?" explanations. |
| R6 | My Settings | `settings` | Email signature, OOO toggle (pauses all plays), notification toggle switches. Autonomy moved to R8. |
| R7 | Weekly Digest | `digest` | Stats, sent-by-play breakdown, replies handled, results vs holdout, top accounts. |
| R8 | My Plays | `plays` | Card grid of 5 enabled plays. Per-play: enrolled count, sends this week, autonomy level, revenue, progress bar. Click → R9. |
| R9 | My Play Detail | `plays` (viewingPlay set) | Play description, step timeline, sample email on real account, enrolled accounts table with Remove, recently exited. Pause for my book toggle. |

### Admin screens (`WizSDR Admin.dc.html`)

| ID | Screen | Nav key | What it does |
|----|--------|---------|-------------|
| A1 | Overview Dashboard | `overview` | Incremental revenue, plays live, team activity, deliverability health, handoff trend chart. |
| A2 | Play Library | `library` | 12-card grid: 5 Live, 3 Ready, 4 Blocked. Each shows status, category, description, revenue or blocked reason. Click → A3. |
| A3 | Play Detail | `library` (viewingAdminPlay set) | Enable/Disable toggle, tunable parameter sliders (±buttons, live audience count), audience preview table, enrolment funnel. |
| A4 | Autonomy Matrix | `autonomy` | 4 reps × 5 plays grid. Readable level names ("Drafts for approval", "Auto-send + spot checks"). Promotion progress. Demote-all with confirmation. Warm-up progress bar. |
| A5 | Brand & Content | `brand` | 5 tabs: Voice (settings + live preview on real account + edit form), Offers (registry table + add form), Claims Policy, Freight & Terms, Calendar/What's New (+ add update form). |
| A6 | Data Connections | `data` | 6 sources with status dots, freshness, play unlocks. Connect/Disconnect toggle per source. |
| A7 | Sending & Deliverability | `sending` | Domain auth (SPF/DKIM/DMARC), connected mailboxes, bounce/complaint rates, breaker state. |
| A8 | Suppression & Consent | `suppression` | Searchable DNC table with reason/source/date. Add entry form (email + reason). Export with feedback. Remove for manual entries. |
| A9 | Results | `results` | Per-play incremental vs attributed revenue, handoff rate, kill rate, confidence intervals. "Not yet significant" states. |
| A10 | Reports | `reports` | Saved reports with PDF/CSV download buttons. |
| A11 | Audit Log | `audit` | Searchable event history: time, action, account, play, rep. |

### Simulator screens (`WizSDR Simulator.dc.html`)

| ID | Screen | Tab key | What it does |
|----|--------|---------|-------------|
| S1 | Control Panel | `control` | Sim date display, +1 Day / +1 Week / Autoplay buttons. Stats update live. Tick summary after each advance. |
| S2 | Inject Events | `inject` | 6 event buttons: new lead, abandoned cart, restock, buyer replies (interested, OOO, order placed). Fire with feedback. |
| S3 | Scenarios | `scenarios` | 16 pass/fail expectations. 14 passing, 2 pending. Each shows scenario, play, expected outcome, result badge. |
| S4 | World Settings | `world` | Lift-per-play ± controls, buyer persona mix (active/occasional/lapsed/new). |
| S5 | Under the Hood | `hood` | Dev tool links (Mailpit, Jaeger, Event Bus, Temporal), LLM token usage, recent event bus activity. |

## Cross-navigation

- **Rep ↔ Admin**: Persona switcher button in top bar header + sidebar "Switch to Admin/Rep" button
- **Rep/Admin → Simulator**: "Simulator" pill in sidebar
- **Simulator → Rep**: "← Exit Simulator" button
- **Router-level**: `WizSDR Prototype.html` has tabs that switch personas via iframe src

## Interactive flows

### Rep
- **Notifications**: Bell icon opens dropdown with 7 items, each navigates to relevant screen
- **Agent Inbox**: Approve → feedback banner + advance to next. Edit/Reject → feedback. Filter tabs.
- **Handoffs**: Send Reply → "✓ Sent" then advance. Dismiss → skip. Contact update confirm button.
- **Account Detail**: Pause/Resume toggle, Kill switch toggle, "Why?" expandable explanations
- **My Settings**: OOO on/off, notification toggle switches (4 toggles)
- **My Plays**: Pause/Resume per play

### Admin
- **Play Detail**: Enable/Disable toggle, ± parameter buttons with live audience count
- **Autonomy**: Demote-all with confirmation dialog, readable level names
- **Brand & Content**: Edit Voice form, Add Offer form, Add Update form (all tabs populated)
- **Data Connections**: Connect/Disconnect per source
- **Suppression**: Add Entry inline form, Export with "✓ Exported" feedback
- **Notifications**: Bell icon with 4 items navigating to relevant screens

### Simulator
- **Control Panel**: +1 Day / +1 Week advance clock, Autoplay toggle (auto-advances every 1.5s), live-updating stats
- **Inject Events**: Fire buttons with "✓ Fired" feedback
- **World Settings**: ± lift adjustments per play

## Synthetic data

Tenant: **Brightwater Lighting Co.** (wholesale lighting)
Rep: **Dana Chen** (48 accounts)
Admin: **Jordan Mitchell**
Team: Dana Chen, Luis Herrera, Kim Tran, Marcus Webb

12 accounts with realistic names, regions, order histories, and statuses. 7 inbox drafts with full email content. 5 handoffs with buyer reply threads and pre-drafted responses. 8 timeline events with "Why?" explanations.

## Source PRD

Full product spec is in `uploads/PRD.md`. Covers:
- 7 user story groups (Setting Up, Governing, Selling, Engaging, Operating, Measuring, Personalising)
- Play engine system design (facts, triggers, audiences, sequences, arbitration)
- 16 plays in the launch set
- Guardrails, autonomy levels (L0–L4), warm-up, earned promotion
- Measurement (incremental revenue, holdouts, CUPED)
