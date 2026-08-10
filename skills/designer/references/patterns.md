# UI Pattern Reference

Patterns for navigation, data-dense screens, forms, integrations, roles, destructive actions, and search. Read before building tables, forms, or workflow screens.

## 1. Navigation and information architecture

Model the domain before drawing the sidebar. Navigation is the visible shape of the information architecture.

### Layers

| Layer | Elements |
|---|---|
| Global | Sidebar, top navigation, breadcrumbs |
| Contextual | Tabs, sections, submenus, related records |
| Local | In-page anchors, step indicators, filters |

### States

Every navigation item implements: active, hover, focus, disabled, collapsed, expanded. Active must be distinguishable without relying on color alone.

### Structure for business systems

Group by business process, not by database table:

```
Dashboard

Sales
 ├── Quotations
 ├── Sales Orders
 ├── Delivery Notes
 └── Invoices

Purchasing
 ├── Requisitions
 ├── RFQs
 ├── Purchase Orders
 └── GRNs

Inventory
 ├── Items
 ├── Warehouses
 └── Stock Movements
```

Rules:

- Roughly seven or fewer top-level groups.
- Two levels of nesting is the practical limit; a third level belongs in tabs on the destination page.
- Breadcrumbs on every detail page: `Purchasing / Purchase Orders / PO-2026-00482`.
- Every screen answers: where am I, how did I get here, where can I go next.

## 2. Data-dense UI

Business applications must prioritize information density without becoming visually cluttered. Do not wrap every piece of information in a giant card.

### Table requirements

| Feature | Requirement |
|---|---|
| Column hierarchy | Primary identifier first, then status, then supporting data, actions last |
| Sticky headers | When the table scrolls beyond a viewport |
| Row hover | Subtle background change, full-row target |
| Sort indicators | Visible current sort column and direction |
| Filters | Above the table, showing active filter count |
| Search | Scoped to the table, with result count |
| Pagination | Page size control plus total record count |
| Column visibility | User can show/hide columns on wide tables |
| Density control | Comfortable and compact row heights |
| Status badges | Consistent color and label mapping across the app |
| Numeric alignment | Right-aligned, tabular figures |
| Currency | Consistent symbol placement and decimals: `SAR 128,450.00` |
| Dates | One format app-wide: `10 Aug 2026` |
| Bulk selection | Header checkbox with indeterminate state |
| Bulk actions | Appear in a contextual action bar when rows are selected |

### Layout

Prefer whitespace, dividers, sections, tables, panels, and tabs over stacking cards. A table is already a container — it does not need a card around it.

## 3. Forms

Forms must be designed around user workflow rather than simply displaying database fields.

### Requirements

- Logical grouping with section headings
- Required field indicators
- Inline validation on blur and on submit, not on every keystroke
- Helpful descriptions where a field is non-obvious
- Correct field types (date picker for dates, combobox for large lists, number input for numbers)
- Sensible defaults
- Clear, specific error messages that say how to fix the problem
- Explicit save and cancel behavior
- Unsaved-change protection when navigating away
- Loading state on submit with the button disabled to prevent double submission
- Success feedback that confirms what happened

### Structure for large forms

```
Basic Information
───────────────

Contact Information
───────────────

Financial Information
───────────────

Additional Information
───────────────
```

Never present forty inputs as one undivided wall. For multi-step flows, show a progress indicator and allow going back without losing data.

### Layout

- Single column for most forms; two columns only for genuinely short, related pairs.
- Labels above fields for scanability.
- Field width reflects expected content length — a postal code field should not be as wide as an address field.

## 4. Integrations

UI design must account for the actual behavior of integrations. Never design a UI that assumes everything always succeeds.

Design explicit handling for:

| Integration | UI considerations |
|---|---|
| API loading | Skeletons matching layout; avoid full-page spinners |
| API errors | Message plus retry; distinguish 4xx from 5xx from network failure |
| Authentication | Session expiry, re-auth prompt, redirect back to intended page |
| Permission states | Hidden vs disabled vs explained; never a blank page |
| File uploads | Progress, size and type validation, cancel, failure retry |
| Notifications | Non-blocking, dismissible, queued rather than stacked infinitely |
| WebSockets | Connection state indicator, reconnect behavior, stale-data handling |
| Search | Debounce, in-flight indicator, no-results state, result count |
| Pagination | Loading state that preserves layout, out-of-range handling |
| Filtering | Active filter chips, clear-all, empty-result state |
| Export | Progress for large exports, download confirmation, failure path |
| Import | Validation preview, per-row error reporting, partial success |
| Printing | Print stylesheet, page breaks, no navigation chrome |
| Email | Send confirmation, failure surfaced to the user |
| PDF generation | Generation progress, preview where useful, failure path |

Every network call has: success, empty, error, and timeout handling. After a successful mutation, refresh or invalidate the affected data so the user never sees stale values.

## 5. Role-based UI

For enterprise systems, account for roles such as admin, manager, employee, viewer, and approver.

Rules:

- Decide deliberately between hiding an action and disabling it. Hide when the user should never see it; disable with an explanation when the user could gain access or the absence would be confusing.
- Approval workflows show current state, who is responsible next, and the history so far.
- Audit information (created by, modified by, timestamps) is available on records that need traceability.
- Never randomly hide things — permission behavior must be consistent and predictable across screens.

## 6. Destructive and confirming actions

Delete, cancel, reject, archive, submit, and approve all need deliberate handling.

Confirmation dialogs restate the specific object and consequence:

```
Delete Purchase Order?

This action cannot be undone.

Purchase Order:
PO-2026-00482

[ Cancel ]  [ Delete Purchase Order ]
```

Rules:

- Never a bare "Are you sure?".
- The confirm button names the action, not "OK".
- Destructive confirm buttons use the danger token and sit away from the safe default.
- Reversible actions prefer an undo toast over a confirmation dialog.
- Approve and reject flows capture a reason where the business process requires one.

## 7. Search and filtering

Search is a first-class feature in business applications.

Support where appropriate:

- Global search across entities, with grouped results
- Page-scoped search
- Filters and advanced filters
- Saved filters
- Recent searches
- Clear filters, individually and all at once
- Visible search result count

Filter state should be reflected in the URL so views are shareable and survive a refresh.

## 8. Component reuse

Never create visually equivalent components multiple times with slightly different implementations.

Before building anything, search the codebase for an existing primitive. Extend it with props rather than forking it. If two components differ only in padding or color, they are one component with a variant.

Required set: buttons, inputs, selects, dropdowns, cards, tables, tabs, badges, avatars, modals, drawers, tooltips, toasts, alerts, breadcrumbs, pagination, search, filters, date pickers, navigation, sidebar, header, empty states, loading states.

Never mix component systems within a file. Never rebuild a primitive the chosen library already provides.
