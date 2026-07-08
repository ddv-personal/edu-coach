[design-system-foundations.md](https://github.com/user-attachments/files/29801368/design-system-foundations.md)
# NVO Prep Coach — Foundational Design System v1.0

**Owner:** Design System & Visual Design Lead
**Companion file:** `design-tokens.css` (implementable source of truth)
**Status:** Foundation layer — colors, type, spacing, radius, elevation, motion, accessibility rules. Components (buttons, cards, forms, progress indicators, etc.) will be built on top of this and documented separately as they're designed.

---

## 1. Design principles this system encodes

Every decision below optimizes for the same short list, in this order:

1. **Calm over stimulating.** 10-14 year old students encountering this during exam prep should feel steadier after looking at the screen, not more activated.
2. **Premium over playful.** Confidence and quality, not gamification. No neon, no bounce, no mascot energy.
3. **Warm over corporate.** This is a private tutor, not enterprise SaaS. Warm neutrals, generous whitespace, softened edges.
4. **One decision, reused everywhere.** A token is a decision made once. If a screen needs a color/spacing value not in this system, that's a signal to extend the system — not to pick a one-off value.

---

## 2. Color system

### 2.1 Primary — Trust / Focus

| Token | Hex | Use |
|---|---|---|
| `--color-primary-900` | `#0F2A4A` | High-emphasis text, dark surfaces |
| `--color-primary-700` | `#1D4E89` | **Main brand color.** Primary buttons, links, active nav/tab states |
| `--color-primary-500` | `#3B72B0` | Hover/pressed states, secondary emphasis |
| `--color-primary-100` | `#E3EDF7` | Selected-row tint, subtle highlight fills |
| `--color-primary-50` | `#F3F7FC` | Faint background wash (e.g. info banners) |

**Why this blue:** deep enough to read as trustworthy and focused (not childish), not so dark it feels somber. It's deliberately restrained — used for interaction and emphasis, never as a large flat background fill, where it would start to feel heavy and institutional.

### 2.2 Accent — Progress / Achievement

| Token | Hex | Use |
|---|---|---|
| `--color-accent-600` | `#C98A2B` | Badge/milestone icons, streak indicators |
| `--color-accent-400` | `#E3A94F` | Lighter badge fills |
| `--color-accent-100` | `#FBEED9` | Achievement callout backgrounds |

**Why gold, and why "reserved":** warm gold reads as "earned," not "childish reward sticker" the way bright orange or neon yellow would. But its power depends on scarcity — if every screen has a gold badge, none of them feel special. **Rule: accent color appears only at genuine milestones** (streak, mission complete, level-up), never as decoration.

### 2.3 Semantic (status) colors

| Token | Hex | Meaning |
|---|---|---|
| `--color-success-600` / `-100` | `#3F8F6C` / `#E1F0E8` | Correct, complete, on track |
| `--color-warning-600` / `-100` | `#B8792E` / `#F6EBDA` | Needs attention, incomplete |
| `--color-error-600` / `-100` | `#B5473D` / `#F7E6E4` | Incorrect, missed, overdue |
| `--color-info-600` / `-100` | (= primary) | Neutral informational message |

**Why muted, not saturated:** a stock "success green" or "error red" is calibrated for adult dashboards under low emotional stakes. For a child doing timed exam practice, a saturated red on a wrong answer reads as alarm; muted terracotta reads as "not quite — try again," which matches the tone the spec calls for ("warm but informative, without vilifying mistakes").

**Hard rule:** color is never the only signal. Every success/warning/error state pairs a color with an icon and a text label, both for colorblind accessibility and because a 12-year-old shouldn't have to decode a color to know if they got something right.

### 2.4 Neutrals

| Token | Hex | Use |
|---|---|---|
| `--color-neutral-900` | `#23201C` | Primary text |
| `--color-neutral-700` | `#4A4540` | Secondary text |
| `--color-neutral-500` | `#8B8580` | Placeholder / disabled / tertiary text |
| `--color-neutral-300` | `#D8D3CC` | Borders, dividers |
| `--color-neutral-100` | `#F2EFEA` | Subtle surface fills |
| `--color-neutral-50` | `#FAF8F5` | App background |
| `--color-surface` | `#FFFFFF` | Card / sheet surfaces |

**Why warm grey, not blue-grey:** blue-grey neutrals (the Tailwind/Material default) are what make products look like generic dashboards. A warm, slightly paper-toned neutral scale is a small change that does a lot of work toward "premium tutor," not "corporate tool."

### 2.5 Contrast requirements

All text/background pairings in this system meet **WCAG AA**: 4.5:1 for body text, 3:1 for large text (≥18px/24px bold) and UI components. `neutral-900` on `neutral-50`/`surface`, and `primary-700` on `surface`/`neutral-50`, both clear this comfortably. Any new color pairing must be checked before use — don't assume a token is safe in a context it wasn't designed for (e.g. accent-400 text on white is *not* AA-compliant; accent is a fill/icon color, not a text color).

---

## 3. Typography

### 3.1 Family

**Inter**, one family for the entire product.

- Full native Cyrillic character support — non-negotiable, since all content is Bulgarian.
- Neutral, geometric-humanist shape: legible at small sizes, doesn't skew playful (like a rounded/geometric display font would) or stiff (like a narrow corporate grotesk would).
- Variable font — one file covers the whole weight range used below.

A second, serif family for printed/parent-report headlines was considered (to add editorial warmth to the twice-weekly parent report) and is **explicitly deferred** — flagged here rather than silently added, since introducing a second family is a system-level decision, not a one-screen choice. If wanted, it should be evaluated once report screens are actually being designed.

### 3.2 Scale

| Token | Size | Line-height | Weight | Use |
|---|---|---|---|---|
| `display` | 32px | 40px | 700 | Rare — hero/welcome moments only |
| `h1` | 28px | 36px | 700 | Screen titles |
| `h2` | 22px | 30px | 600 | Section headers |
| `h3` | 18px | 26px | 600 | Card titles, subsections |
| `body-lg` | 17px | 26px | 400 | Exercise prompts, reading passages |
| `body` | 15px | 24px | 400 | Default UI text |
| `body-sm` | 13px | 20px | 400 | Secondary info, metadata |
| `label` | 13px | 16px | 600 | Buttons, tags, form labels (0.01em tracking) |
| `caption` | 12px | 16px | 400 | Timestamps, helper text |

**Why body is 17px, not 14–16px:** the primary readers are 10–14-year-olds doing sustained reading-comprehension and math-reasoning work. A larger base size reduces eye strain over a 30–45 minute session and is a genuine accessibility choice — it doesn't need to look "kids-app large," just comfortably above default web body size.

**Why so few weights:** only 400/600/700 are used anywhere. Hierarchy comes from size and color (primary vs. secondary text), not from a wide range of font weights — fewer weight decisions means less visual noise and a system that's easier to keep consistent as new screens are added.

---

## 4. Spacing — 8pt grid

Base unit: 4px. Every margin, padding, and gap in the product should map to one of these tokens — no arbitrary pixel values in component code.

| Token | Value | Typical use |
|---|---|---|
| `space-2xs` | 4px | Icon-to-label gap |
| `space-xs` | 8px | Compact internal padding |
| `space-sm` | 12px | Form field internal padding |
| `space-md` | 16px | Default component padding / base gap |
| `space-lg` | 24px | Card padding, spacing between related elements |
| `space-xl` | 32px | Spacing between distinct content groups |
| `space-2xl` | 48px | Section breaks |
| `space-3xl` | 64px | Major page-level separation |
| `space-4xl` | 96px | Empty-state / hero vertical rhythm |

**Why this matters more than color:** an inconsistent color is noticeable; inconsistent spacing is what actually makes a product feel "different designers built different screens," even when the colors and fonts match. This is the single highest-leverage rule in the system — it's also the easiest one to accidentally violate by eyeballing a value instead of picking a token.

---

## 5. Radius

| Token | Value | Use |
|---|---|---|
| `radius-sm` | 8px | Inputs, chips, small controls |
| `radius-md` | 12px | Buttons, default card radius |
| `radius-lg` | 20px | Large cards, modals, sheets |
| `radius-full` | 999px | Pills, avatars, badges |

Soft enough to feel approachable; not so rounded (e.g. 24px+ on everything) that it reads as an app built for toddlers.

---

## 6. Elevation

| Token | Value | Use |
|---|---|---|
| `shadow-1` | `0 1px 2px rgba(35,32,28,.06)` | Resting card |
| `shadow-2` | `0 4px 12px rgba(35,32,28,.08)` | Raised / hover state |
| `shadow-3` | `0 12px 32px rgba(35,32,28,.14)` | Modal / overlay |

Shadows are tinted with the neutral-900 warm charcoal, not pure black — softer, more paper-like. Elevation should communicate "this is on top of / floating above the page," not be used decoratively on elements that don't need it.

---

## 7. Motion

| Token | Value |
|---|---|
| `duration-fast` | 120ms |
| `duration-base` | 200ms |
| `duration-slow` | 320ms |
| `easing-standard` | `cubic-bezier(0.4, 0, 0.2, 1)` |
| `easing-emphasized` | `cubic-bezier(0.2, 0, 0, 1)` |

**Hard rule: no spring/bounce easing anywhere in the product.** Bounce is the single fastest way to make an interface feel like a game rather than a calm, focused tool — it directly contradicts the brand's "confidence and clarity" goal. All motion should settle, not bounce.

---

## 8. Accessibility baseline

- All text/background pairs meet **WCAG AA** (4.5:1 body, 3:1 large text/components).
- Minimum touch target: **44×44px** — students will use this on phones.
- Visible focus state on every interactive element: `2px solid primary-700`, `2px` offset. Never remove the default focus ring without providing this replacement.
- Status is never color-only — always color + icon + text.
- Motion respects `prefers-reduced-motion` — durations should collapse toward instant when set.

---

## 9. Naming convention

`--{category}-{role or scale-step}`, e.g. `--color-primary-700`, `--space-lg`, `--font-size-h2`. Color tokens use numeric scale steps (100–900) so intermediate values can be added later without renaming; spacing and type tokens use role-based names (`lg`, `h2`) so components read intention rather than a raw number.

---

## 10. Governance

- No component should hardcode a hex, px, or font-size value. If a value isn't in `design-tokens.css`, that's a request to extend the system, raised before it's used.
- Any new screen gets checked against this file before build, not after.
- This is v1.0 — foundation only. Next layer is component-level documentation (buttons, cards, inputs, progress indicators, empty/error/success states) built on top of these tokens.
