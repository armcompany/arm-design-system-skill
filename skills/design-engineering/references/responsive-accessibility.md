# Responsive & Accessibility Checklists

## Responsive

Define per screen, in the spec — never as an afterthought, never only "mobile = stacked cards".

For each relevant breakpoint (mobile / tablet / laptop / desktop / ultrawide), decide:

- what collapses (sidebar → drawer, filters → sheet)
- what moves (inspector below canvas, actions into overflow menu)
- what becomes bottom navigation or tabs
- what becomes horizontally scrollable (wide tables, kanban)
- what remains persistent (primary nav, critical actions)
- touch targets and hover-dependent interactions replaced on touch

Complex desktop systems (GIS, ERP, dashboards) may legitimately require a desktop-minimum with a constrained mobile read-only mode instead of a naive squeeze — decide explicitly and record it.

## Accessibility (minimum bar)

- Semantic heading/landmark hierarchy
- Full keyboard operability; logical tab order; no keyboard traps
- Visible focus states (not `outline: none` without replacement)
- Contrast: 4.5:1 body text, 3:1 large text/UI
- Every input labelled; errors announced and tied to fields
- Interactive targets ≥ 44×44px
- ARIA only where semantics are insufficient; correct roles on custom widgets
- Screen-reader behavior for dynamic regions (toasts, async results, modal open/close)
- `prefers-reduced-motion` honored
- Status conveyed by more than color alone (icon + text)

Accessibility is never sacrificed for aesthetics; find the aesthetic solution that meets the requirement.
