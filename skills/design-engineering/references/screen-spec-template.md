# Screen Specification Template

One file per screen: `design/screens/SCR-xxx-name.md`. This is the contract for renderers, implementers, and QA. Missing required product behavior is a defect; approved design-system defaults, semantics, focus behavior, and platform plumbing belong in **Allowed baseline**.

```markdown
# SCR-000 — <Screen name>

- Route: /path/:param
- Role(s): <who can see it>
- Priority: P0/P1/P2
- Spec version: v1 (date)
- Requirement sources: <PRD/story/API/reference>

## User and entry context
- Primary user: <role, goal, constraints>
- Entry point and preconditions: <route, prior action, permission/data>

## Purpose
<What the user accomplishes here, one sentence.>

## Layout
- <Region>: <dimensions/behavior>  (e.g., Global sidebar 240px, main canvas fluid, right inspector 420px)

## Required components
- <component>: <what it shows / binds to>

## Actions
- <action>: <trigger> → <result>

## States
- loading: <behavior> | N/A: <reason>
- empty: <behavior> | N/A: <reason>
- loaded: <behavior> | N/A: <reason>
- partial data / degraded: <behavior> | N/A: <reason>
- permission denied: <behavior> | N/A: <reason>
- error: <behavior and recovery> | N/A: <reason>

## Responsive behavior
- <breakpoint>: <what collapses / moves / persists>

## Accessibility
- <focus order, labels, announcements, targets>

## Data requirements
- <entities/fields this screen consumes; where they come from>

## Allowed baseline
- Approved components/tokens: <names or source>
- Necessary semantic, focus, screen-reader, and platform behavior: <what is allowed>

## Decision-required items
- <owner>: <question, status>

## PROHIBITED product changes
- No <invented widgets / metrics / AI features / nav items / attributes>
- No <behavior or content beyond the approved spec or allowed baseline>

## Acceptance evidence
| Requirement | Evidence | Status |
|---|---|---|
| <spec item> | <screenshot, runtime check, or review> | Planned |
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
