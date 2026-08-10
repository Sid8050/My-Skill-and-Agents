# Design Review Reference

The self-review, scoring rubric, and screenshot workflow. Run this before declaring any UI task complete.

## 1. Review workflow

```
Implement → Self-review checklist → Fix findings → Screenshot test → Fix findings → Score → Report
```

Do not stop after writing code. An unreviewed UI is an unfinished UI.

## 2. Self-review checklist

Walk every item. For each failure, record the file, the problem, and the fix — then apply the fix.

```
DESIGN REVIEW

Foundation
□ Visual hierarchy — the most important thing on screen reads first
□ Typography — scale roles used correctly, no arbitrary sizes
□ Spacing consistency — all values from the scale
□ Color consistency — semantic tokens only, zero hardcoded values
□ Icon consistency — one library, one stroke width, consistent sizes
□ Component reuse — no duplicate near-identical components
□ No unnecessary cards — no nested cards, no card around every element
□ No inconsistent styling — one radius set, one border treatment, one shadow set

Themes
□ Light mode — complete and correct
□ Dark mode — designed independently, surface ladder correct, not inverted
□ Contrast passes in both themes against actual surfaces

States
□ Loading states — skeletons match real layout
□ Empty states — explanation plus primary action
□ Error states — explanation plus recovery action
□ Hover states — on every interactive element
□ Focus states — visible, keyboard reachable
□ Disabled states — visually clear, reason given where non-obvious

Structure
□ Navigation — IA is coherent, breadcrumbs present, active state clear
□ Forms — grouped, validated, protected against unsaved loss
□ Tables — sorting, filtering, pagination, alignment, density
□ Permissions — hide vs disable decided deliberately and applied consistently

Delivery
□ Responsive behavior — mobile, tablet, laptop, desktop, large desktop
□ Mobile UX — not a shrunken desktop layout
□ Accessibility — keyboard, semantics, labels, contrast, no color-only meaning
```

## 3. Scoring rubric

Score each category out of 10. Anything below 8 gets fixed before handoff, not logged as a follow-up.

```
DESIGN QUALITY SCORE

Visual hierarchy       /10
Typography             /10
Spacing                /10
Color system           /10
Navigation             /10
Interaction design     /10
Responsive design      /10
Accessibility          /10
Dark mode              /10
Consistency            /10
────────────────────────
Total                  /100
```

### Category criteria

| Category | 8+ means |
|---|---|
| Visual hierarchy | Primary action and key data are obvious within two seconds; secondary content recedes |
| Typography | Every text element maps to a defined role; tabular figures on data; no arbitrary sizes |
| Spacing | All values from the scale; tight within groups, generous between them; consistent page rhythm |
| Color system | Semantic tokens only; one primary; status colors reserved for status |
| Navigation | IA matches the domain; breadcrumbs and active states present; no orphan pages |
| Interaction design | All seven interaction states on every interactive element; motion is purposeful and reduced-motion aware |
| Responsive design | Each breakpoint is a deliberate layout, not a scaled-down desktop; tables adapt intentionally |
| Accessibility | Keyboard complete, focus visible, WCAG AA contrast, semantic HTML, no color-only meaning |
| Dark mode | Independently designed surface ladder; charts, tables, inputs, and borders re-tuned |
| Consistency | One radius set, one shadow set, one icon library, reused components throughout |

**Do not consider the task complete if the design has obvious issues.** Report the score with the task summary.

## 4. Screenshot test

When browser or screenshot tooling is available, never assume the code is visually correct.

```
Build → Run → Screenshot → Inspect → Identify visual issues → Fix → Screenshot again
```

Capture at minimum:

- Light mode and dark mode
- Desktop width and mobile width
- The primary screen plus one dense screen (a table or a long form)
- At least one non-happy state (empty or error)

### What to look for in a screenshot

Things that pass code review and fail visually:

- Misaligned baselines between icons and text
- Inconsistent vertical rhythm between sections
- Columns that collide or truncate with realistic data
- Contrast that reads fine in tokens but fails against the actual surface
- Focus rings clipped by overflow containers
- Shadows that disappear or halo in dark mode
- Buttons of different heights sitting side by side
- Text wrapping into awkward orphans at common widths

Iterate until the screenshot matches the intent, not just until the code compiles.

## 5. Reporting format

```markdown
## Design Review — [Screen or Feature]

### Score: NN/100
[Category table with any score below 8 called out]

### Fixed during review
- [Issue] → [fix applied], file:line

### Remaining risks
- [Anything that needs a product decision rather than a design fix]
```

If any category scores below 8 and cannot be fixed within the current task, say so explicitly rather than reporting the work as complete.
