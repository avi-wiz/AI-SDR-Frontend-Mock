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
WizSDR Prototype.html             ← Entry point: persona router (tabs load DC files in iframe)
├── WizCRM Sales Agents.dc.html   ← Rep screens (R1–R9)
├── WizSDR Admin.dc.html          ← Admin screens (A1–A11)
├── WizSDR Simulator.dc.html      ← Simulator screens (S1–S5)
├── assets/
│   ├── wiz-logo-white.png        ← Inverse logo for dark header
│   └── wiz-mark-white.svg        ← Mark for dark header
├── uploads/PRD.md                ← Source PRD (full spec)
└── _ds/...                       ← Design system (tokens, fonts, bundle)
```

Each `.dc.html` file is a Design Component — a single self-contained file with an HTML template and a JS logic class. They render directly in a browser with `support.js`.

## Synthetic data

Tenant: **Brightwater Lighting Co.** (wholesale lighting distributor)
Rep: **Dana Chen** (48 accounts)
Admin: **Jordan Mitchell**
Team: Dana Chen, Luis Herrera, Kim Tran, Marcus Webb

12 accounts with realistic names, regions, order histories, and statuses. 7 inbox drafts with full email content and email threads. 5 handoffs with buyer reply threads and pre-drafted responses. 8 timeline events with "Why?" explanations. 5 unique play details with step timelines, sample emails, enrolled accounts, and exit data.

## Source PRD

Full product spec is in `uploads/PRD.md`. Covers:
- 7 user story groups (Setting Up, Governing, Selling, Engaging, Operating, Measuring, Personalising)
- Play engine system design (facts, triggers, audiences, sequences, arbitration)
- 16 plays in the launch set
- Guardrails, autonomy levels (L0–L4), warm-up, earned promotion
- Measurement (incremental revenue, holdouts, CUPED)
