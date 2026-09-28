# WizCommerce Design System

The WizCommerce design system in one place. Tokens, type, color, components, brand. Use this any time you build something that wears the WizCommerce name.

---

## Who this is for

Designers and engineers building **WizCommerce** product surfaces, marketing sites, decks, and emails. The system covers everything from a 12px badge to a hero headline.

---

## Company in one paragraph

WizCommerce is a wholesale OS for B2B distributors and manufacturers. The product line includes **WizOrder** (sales rep app + order desk), **WizShop** (B2B ecommerce catalog), and **WizAI** (agents that quote, follow up, and reconcile). The core customer is a small-to-mid-market wholesale operator drowning in spreadsheets and email — the brand's job is to feel like a calm, capable colleague who already did the work.

---

## Visual foundations

| File | What's inside |
|---|---|
| `tokens.css` | Single source of truth — every color, font, space, radius, shadow as CSS variables. **Import this first** in any artifact. |
| `brand.html` | Logo lockups, mark, clear space, voice. |
| `colors.html` | Wiz Orange, ink neutrals, brand surfaces, the no-semantic-color status pattern, approved pairings. |
| `type.html` | Recife (display), General Sans (UI), Geist Mono (numerics). Full scale. |
| `space.html` | 4px spacing scale, radii, elevation, density modes, layout grid. |
| `icons.html` | 24px outline icons, 2px stroke, currentColor. Library + anatomy. |
| `components.html` | Buttons, inputs, badges, tables, stat tiles, product cards, tabs. |

---

## Content fundamentals

**Tone.** Direct, specific, quietly confident. We're talking to ops people who don't have time for hype.

**Headlines.** Recife serif, often with one italicized phrase doing emotional work. Numbers belong in headlines as words — “Quote 12,400 SKUs before lunch” beats “Faster quoting.” But the figures themselves are typeset in Geist Mono, never Recife.

**Body copy.** General Sans, 15px default. One idea per paragraph. Verbs first.

**Numbers.** Always **General Sans Medium (500)** with `letter-spacing: -0.01em` and tabular figures (`font-feature-settings: "tnum" 1, "lnum" 1`). One recipe, one weight, one tracking value. Geist Mono is for identifiers (SKUs, refs, hex codes, code), not for numerals. Currency uses commas, two decimals: `$24,500.00`.

**Forbidden.** "Revolutionary," "next-gen," "AI-powered everything," "seamless," "leverage," "robust," gratuitous emoji.

---

## Color rules

- **Wiz Orange (#FE7630)** is the loudest thing on a screen. Use it once, where it matters most: the primary CTA, the lead metric, an active nav item.
- Never use orange as a long-form background or for body text.
- **No semantic colors.** No green for success, red for error, amber for warning, blue for info. Status is communicated through copy and hierarchy on a square ink-900 box. Wiz Orange remains the only color that signals "act on this," and only on the actionable element.
- The dominant surfaces are `ink-0` (white), `ink-50` (off-white), and `wiz-orange-600` (canvas). Type on all three is `ink-900`. **Type on orange-600 is always black (ink-900) — no exceptions.** No white text on the brand orange, not as eyebrows, not as buttons, not as captions, not "sparingly." If you need contrast against orange, lift type onto a peach card (orange-50). Black-canvas sections are rare; reach for them only on the inverse mark/lockup pages.
- **Backgrounds are always plain.** No grids, no cross-hatch, no dot patterns, no noise, no gradients, no textures of any kind. Every brand surface — orange-600, peach, ink-50, ink-0, sand, lilac — is a single flat fill. Depth comes from hairlines and type hierarchy, not from background pattern.
- **Slide canvas: white, off-white, or Wiz Orange — never black.** Black is for type, not backgrounds. Decks run on the same surfaces as everything else; the brand never appears on a full-black slide.

---

## Layout rules

- **Hairlines do the structural work.** WizCommerce builds layouts with 1px lines, not boxes. Hairlines define columns, separate rows, and frame slide regions — no card backgrounds, no shadows, no padding boxes for default structure.
- Default rule weight is `1px var(--border-subtle)` (ink-200). Step up to `--border-strong` (ink-300) only for the edge of a major region — slide frame, modal, side panel.
- Hairlines bleed edge-to-edge of their section or slide. No gutters at the ends.
- Never combine a hairline with a shadow or a tinted card on the same surface — pick one structural device and commit.
- The system is square. Buttons, inputs, cards, panels, sections, tables, tiles, modals, images: `border-radius: 0`. Pills are reserved for true circles (avatars, dots, switches).

---

## Typography rules

- **Recife** — display only, **always Book (weight 300)**. Hero headlines, page titles, taglines, slide titles. Never Regular, never SemiBold, never Bold — Book is the only headline weight. **Never used for numbers, statistics, or data values.**
- **General Sans** — everything else. UI, body, buttons, labels, **and every numeral.**
- **Numerals** — General Sans Medium (500), `letter-spacing: -0.01em`, `font-feature-settings: "tnum" 1, "lnum" 1`. Reach for the `.t-num` token in `tokens.css` and override `font-size` per context. Stats, KPIs, prices, percentages, dates, table cells — all sans, never mono.
- **Geist Mono** — reserved for **code and identifiers**: SKUs, order IDs, refs, file paths, hex codes, and the eyebrow recipe. Not for numbers.
- Mixing: pair Recife display with General Sans body. Recife inside a button is a smell.

---

## Number rules

**One recipe.** Every number in the system uses the same setting: General Sans, Medium (500), letter-spacing -0.01em, with tabular and lining figures forced on.

```css
.t-num {
  font-family: var(--font-sans);
  font-weight: 500;
  letter-spacing: -0.01em;
  font-feature-settings: "tnum" 1, "lnum" 1;
}
```

- **Family.** General Sans — same family as body. Numbers are not a separate typeface.
- **Weight.** 500 (Medium). Always. Never 400, never 600.
- **Tracking.** `-0.01em` at every size. At 64px+ display, `-0.02em` is allowed for optical balance. Never positive.
- **Figures.** Tabular and lining (`tnum` + `lnum`) are non-negotiable. Numbers must align vertically in tables, stat grids, and price lists.
- **Color.** Ink-900 by default. Wiz Orange-600 for the lead metric on a dashboard or the hero stat in a marketing block.
- **What this replaces.** Every previous use of Geist Mono on numerics — `45%`, `$24,500.00`, `12,400`, `28d`, dashboard tiles, table number columns. Mono is for identifiers, never for the numeric value itself.

If it's a fixed-glyph string (SKU, ID, hex, file path, code), use Geist Mono. If it's a number you'd do math on, it's `.t-num`.

**Stat-trio constraint.** Every stat-trio module — the three-up marketing numerics block (`.stat-trio`) — uses **General Sans Medium** for the numerals. Never Geist Mono, never Recife. The numerals follow the `.t-num` recipe at 64px with `-0.02em` tracking. Same constraint applies to dashboard stat tiles, deck stat splits, hero KPIs, and any other multi-stat module: if it's a number, it's General Sans.

---

## Button rules

**Two variants. One rule.** Primary is black fill, white text, zero radius — the action you want clicked. Secondary is white fill, 1.5px black stroke, black text — the recede-able partner (Cancel, Back, Save draft, Skip). Same shape, same height, same type. **One primary per region, never two.**

- **Default size:** 56px tall, 24px horizontal padding.
- **Small size:** 40px tall, 16px horizontal padding. Used inside dense product UI.
- **Hover:** primary lightens fill to `--ink-700`. Secondary lightens fill to `--ink-50`. No movement, no scale, no shadow.
- **Focus:** 3px Wiz Orange halo at 32% opacity. `:focus-visible` only.
- **Disabled:** 35% opacity. Same shape.
- **On dark surfaces:** invert. Primary becomes white fill, black text. Secondary becomes transparent fill, 1.5px white stroke, white text.
- **Pairing:** primary + secondary, in that order. Primary right-aligned in modals, primary first in inline rows. Never two primaries side-by-side.
- **No third variant.** No orange button. No rounded corners. No ghost / text-button styled like a button. If an action needs to recede further than secondary, make it a text link.

---

## Iconography rules

- 24px frame, 2px stroke, rounded caps and joins.
- Outline only — no fills, no two-tone.
- Inherits `color` from parent — never hardcode hex inside an SVG.
- Three sizes: 16 (dense), 20 (default), 24 (feature). At 32+, drop the stroke to 1.6px.

---

## File structure

```
.
├── tokens.css                  ← import first
├── fonts/                      ← all brand fonts (woff2/otf/ttf)
├── assets/
│   ├── wiz-logo.png            ← primary lockup
│   ├── wiz-logo-white.png      ← inverse lockup
│   ├── wiz-mark.png            ← cube only
│   ├── product-*.png           ← sample product imagery
│   ├── customer-*.png          ← customer logo placeholders
│   └── screenshot-*.png        ← in-product screenshots
├── brand.html                  ← brand card
├── colors.html
├── type.html
├── space.html
├── icons.html
├── components.html
└── README.md                   ← this file
```

---

## Using the system in a new artifact

```html
<!doctype html>
<html lang="en">
<head>
  <link rel="stylesheet" href="tokens.css">
</head>
<body>
  <h1 class="t-display-lg">A modern wholesale OS</h1>
  <p class="t-body-lg">Built for the people behind the orders.</p>
  <button class="btn">New order</button>
</body>
</html>
```

Tokens are CSS variables: reach for `var(--wiz-orange-600)`, `var(--font-serif)`, `var(--space-6)`, `var(--radius-md)`, `var(--shadow-resting)`. If you need a value that doesn't exist as a token, the token is missing — add it before hardcoding.
