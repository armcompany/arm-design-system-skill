---
name: design-engineering
description: Use when turning product requirements, existing application context, or approved visual references into an implementation-ready product design or bounded redesign. Not for audit-only reports or framework-specific implementation.
---

# Design Engineering

## Core rule

Create a traceable Design Specification before rendering or implementing UI. The specification is authoritative; Figma, generators, image tools, and browser automation produce candidates only. Candidates must not invent or remove product behavior, roles, permissions, navigation, terminology, domain data, metrics, integrations, or AI features.

Design Engineering owns UX and acceptance criteria. Frontend owners implementation. Do not edit application code unless separately authorized.

## Choose the smallest mode

| Mode | Required output | Boundary |
|---|---|---|
| Greenfield, change, recreation, redesign | Brief, IA/flows, direction, system contract, inventory, and screen specs scaled to scope | Inspect existing behavior before changing it. |
| Single screen | Scoped input record and one complete screen spec | No project-wide docs unless shared navigation, entities, or system contracts change. |
| Audit only | Evidence-backed issue report | Do not create replacement UI or change code unless asked. Use a dedicated audit skill when available. |
| Implementation QA | Validation report and correction tasks against an approved spec | A screenshot is not proof of behavior; source changes need authorization. |

## Start from evidence

Read applicable repository instructions and inspect supplied requirements, code, APIs/schema, design system, screenshots, and references. Mark important facts as **KNOWN**, **INFERABLE**, **UNKNOWN**, or **DECISION_REQUIRED**.

Permissions, security, irreversible actions, policy, and material user outcomes marked `DECISION_REQUIRED` need an accountable decision. Surface and record the question; never turn an unapproved assumption into product copy, flow, mockup, or implementation instruction. Research only when it answers a stated question and is permitted; do not transmit private inputs to external services.

## Build the contract before visuals

For a full product change, define IA/navigation, per-role flows, design direction, and the smallest necessary design-system change before producing screens. Reuse the existing system. If `design-system-engineering` is available, invoke it for token/component changes; otherwise record the change and migration impact.

For every rendered or handed-off screen, including a single screen, use [references/screen-spec-template.md](references/screen-spec-template.md). It must define user/entry context, required behavior and states, responsive and accessibility behavior, data needs, open decisions, and acceptance evidence.

The spec defines an **allowed baseline**: approved components/tokens plus necessary semantic, focus, and platform plumbing. Treat an addition as a discrepancy only when it changes visible product content, behavior, information architecture, navigation, or a stated requirement.

## Render, validate, hand off

Rendering is optional. Use an installed, authorized tool only when it improves the outcome; otherwise the spec is the deliverable. Send one bounded screen problem at a time. If the tool changes the contract repeatedly, stop using it and hand off from the spec.

Before acceptance, follow [references/validation.md](references/validation.md) and trace each required item to evidence. Record `PASS`, `FAIL`, `WAIVED`, or `NOT RUN`; unavailable runtime or breakpoint checks are not passes. Use [references/design-direction.md](references/design-direction.md) for direction and [references/responsive-accessibility.md](references/responsive-accessibility.md) for screen expectations.

Handoff includes component tree, data, interactions/outcomes, states, responsive/accessibility behavior, unresolved decisions, and evidence. Implementation deviations become correction tasks or approved waivers, never silent design changes.
