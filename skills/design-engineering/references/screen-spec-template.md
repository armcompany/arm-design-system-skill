# Screen Specification Template

One file per screen: `design/screens/SCR-xxx-name.md`. This is the contract: generative tools, implementers, and QA are all bound to it. Anything not listed here that appears in output is a hallucination; anything listed here that is missing is a defect.

```markdown
# SCR-000 — <Screen name>

- Route: /path/:param
- Role(s): <who can see it>
- Priority: P0/P1/P2
- Spec version: v1 (date)

## Purpose
<What the user accomplishes here, one sentence.>

## Layout
- <Region>: <dimensions/behavior>  (e.g., Global sidebar 240px, main canvas fluid, right inspector 420px)

## Required components
- <component>: <what it shows / binds to>

## Actions
- <action>: <trigger> → <result>

## States
- loading: …
- empty: …
- loaded: …
- partial data / degraded: …
- permission denied: …
- error: …

## Responsive behavior
- <breakpoint>: <what collapses / moves / persists>

## Accessibility
- <focus order, labels, announcements, targets>

## Data requirements
- <entities/fields this screen consumes; where they come from>

## PROHIBITED
- No <invented widgets / metrics / AI features / nav items / attributes>
- No <anything else not in spec>
```

## Component tree (handoff format)

Include in the spec or alongside it:

```
PropertyDetailsPage
├── GlobalSidebar
├── MapCanvas
│   ├── ParcelLayer
│   └── MapControls
└── PropertyInspector
    ├── PropertyHeader
    ├── PropertyMetadata
    ├── ZoningSection
    ├── DocumentsSection
    └── TimelineAction
```
