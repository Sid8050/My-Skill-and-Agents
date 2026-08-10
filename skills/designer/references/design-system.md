# Design System Reference

Token, color, dark mode, typography, spacing, and icon rules. Read before defining or extending a design system.

## 1. Brownfield vs greenfield

Scan first:

1. `components.json` → shadcn project; tokens live in `globals.css` under `:root`
2. `tailwind.config` → `theme.extend.colors`
3. `globals.css` / `app/globals.css` → CSS custom properties
4. `package.json` → shadcn, Radix, MUI, Chakra, Panda CSS, vanilla-extract

If any exist, this is **brownfield**: catalog the tokens and use them. Only add tokens for genuinely missing roles, and harmonize new values with what exists. Do not introduce a second color system.

If none exist, this is **greenfield**: derive the full system below before writing UI.

## 2. Color

### Separate raw from semantic

Raw values are defined once. Application code references semantic tokens only.

```css
:root {
  /* raw scale — defined once, never used directly in components */
  --blue-600: oklch(0.55 0.16 255);

  /* semantic — this is what components use */
  --color-background: oklch(0.99 0 0);
  --color-surface: oklch(1 0 0);
  --color-surface-elevated: oklch(1 0 0);
  --color-border: oklch(0.92 0 0);
  --color-text-primary: oklch(0.20 0 0);
  --color-text-secondary: oklch(0.45 0 0);
  --color-text-muted: oklch(0.60 0 0);
  --color-primary: var(--blue-600);
  --color-success: oklch(0.60 0.14 150);
  --color-warning: oklch(0.72 0.15 75);
  --color-danger: oklch(0.58 0.20 25);
  --color-info: oklch(0.62 0.12 240);
}
```

Zero hardcoded hex, rgb, hsl, or oklch values in JSX, templates, or component styles. If a color is needed that no token covers, add a token.

### Required roles

Primary, secondary, accent, background, surface, elevated surface, border, text primary, text secondary, muted text, success, warning, error, info.

### Corporate palette discipline

One primary brand color. Accents are controlled and few. Status colors (success, warning, danger, info) are reserved for status — never decorative. Neutrals carry the majority of the interface.

## 3. Dark mode

Dark mode must **not** simply invert the light theme. Design it independently.

### The surface ladder

Elevation in dark mode is communicated by getting lighter, not by shadows. Never use pure `#000000` as the page background.

```
Page              oklch(0.16 0 0)   darkest
  ↓
Surface           oklch(0.19 0 0)
  ↓
Elevated surface  oklch(0.23 0 0)
  ↓
Modal / popover   oklch(0.26 0 0)   lightest
```

### Per-element checklist

Independently verify each of these in dark mode rather than assuming the token swap handled it:

| Element | What to check |
|---|---|
| Contrast | Text meets WCAG AA against its actual surface, not against the page |
| Surface elevation | Each layer is visibly distinct from the one beneath |
| Borders | Visible but not harsh; often lighter and lower-contrast than in light mode |
| Shadows | Weaker or replaced entirely by surface lightness |
| Text brightness | Pure white body text is too harsh — step it down |
| Disabled states | Still readable, still clearly disabled |
| Charts | Series colors re-tuned for a dark ground; gridlines dimmed |
| Tables | Row striping and hover re-tuned; borders often replace stripes |
| Inputs | Field background distinct from surface; placeholder still legible |
| Modals, dropdowns, tooltips, notifications | Sit above their parent on the ladder |

### Theme parity rule

Every component ships working in both themes at the same quality. A component that only looks right in one theme is unfinished.

## 4. Typography

Establish the type system before designing screens.

### Family

Pick one family based on product personality. Do not mix families randomly; a second family is only justified for a distinct role such as monospaced data.

| Family | Personality |
|---|---|
| Inter | Neutral, dense, workhorse UI |
| Geist | Modern, technical, product-forward |
| IBM Plex Sans | Institutional, engineered, trustworthy |
| Manrope | Warm geometric, approachable |
| Plus Jakarta Sans | Contemporary, slightly expressive |

### Scale

Define every role explicitly with size, weight, line height, and letter spacing.

| Role | Typical size | Weight | Line height | Tracking |
|---|---|---|---|---|
| Display | 48–60px | 600–700 | 1.05–1.15 | tight |
| H1 | 32–36px | 600 | 1.2 | tight |
| H2 | 24–28px | 600 | 1.25 | normal |
| H3 | 20px | 600 | 1.3 | normal |
| Body | 14–16px | 400 | 1.5–1.6 | normal |
| Small | 13px | 400 | 1.5 | normal |
| Caption | 12px | 400–500 | 1.4 | slight positive |
| Label | 12–13px | 500 | 1.3 | slight positive |
| Button | 14px | 500–600 | 1 | normal |
| Numeric / data | 13–14px | 400–500 | 1.4 | tabular figures |

### Rules

- Numeric and tabular data uses tabular figures (`font-variant-numeric: tabular-nums`) so columns align.
- Maximum line width for reading text is roughly 60–75 characters.
- Sentence case for headings, labels, buttons, and tabs. No ALL CAPS as a hierarchy substitute, no Title Case everywhere.
- Hierarchy comes from size, weight, and color together — not from size alone.

## 5. Spacing

One scale, used everywhere:

```
4  8  12  16  20  24  32  40  48  64  80
```

Never use arbitrary values such as `margin: 13px`, `padding: 17px`, or `gap: 23px` unless there is a genuine, stated design reason (optical alignment, matching a fixed asset).

Rhythm rules:

- Tight spacing within a group, generous spacing between groups. Related things sit closer than unrelated things.
- Vertical rhythm is consistent across pages; the same section spacing everywhere.
- Do not use the same padding on every element — that reads as undesigned.

## 6. Radius, borders, shadows

- **Radius:** pick two values (for example 6px for controls, 10px for containers) and use only those. Inconsistent radius is one of the loudest amateur tells.
- **Borders:** 1px, low contrast, semantic token. No colored side stripes as accents.
- **Shadows:** subtle and few. Reserve them for genuinely floating layers (dropdown, popover, modal). No glow effects.

## 7. Icons

One library for the entire application: **Lucide**, **Phosphor**, or **Heroicons**. Never mix libraries. Never use emoji as UI icons.

Requirements:

- Consistent stroke width across every icon in the app
- Consistent size per context (typically 16px inline, 20px in navigation, 24px in empty states)
- Optically aligned with adjacent text baselines
- Semantic meaning; an icon does not replace text when the meaning is not obvious
- Icon-only actions have a tooltip and an accessible label

## 8. Charts and data visualization

- Series colors derive from the palette and stay consistent across the whole app for the same series.
- Re-tune for dark mode; do not reuse light-mode series colors unchanged.
- Never rely on color alone — pair with labels, patterns, or direct annotation.
- Axis, gridline, and tick styling uses muted text and border tokens, not full-contrast text.
