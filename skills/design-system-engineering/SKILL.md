---
name: design-system-engineering
description: Use when creating, consuming, auditing, or evolving a product Design System with tokens, themes, components, accessibility contracts, Storybook, and safe migration governance.
---

# Design System Engineering

## Overview

Treat the Design System as a product contract between design and code. Establish only the foundation the product needs, prove it on representative screens, and promote recurring patterns deliberately.

## Workflow

1. Inspect existing tokens, themes, components, Storybook, Figma references, tests, and platforms.
2. Reuse and evolve an existing system. Never introduce a competing token namespace or component library without recording the incompatibility and migration path.
3. Define the smallest coherent token layers:
   - raw primitives: palette, type scale, spacing, radius, elevation, motion;
   - semantic tokens: surface, text, border, focus, status, interactive;
   - component tokens: only where a component needs a stable contract.
4. Build components around a clear API, variants, states, and semantics.
5. Keep product-specific components separate from generic primitives. Promote a pattern only after recurrence and a real consumer prove it.
6. Validate with one simple screen, one data-heavy screen, one form-heavy screen, and one critical workflow when those screens exist.
7. Record breaking changes, deprecations, migrations, and platform differences.

## Contract and evolution

### Implementation contract

- UI consumes semantic tokens; raw color and spacing literals require a documented exception.
- Themes provide the same semantic contract across light/dark and supported platforms.
- Components expose named variants instead of forcing consumers to override internals.
- Document tokens, components, and accessibility behavior close to their source.
- Domain logic remains outside presentational components and the Design System.

### Breaking changes and compatibility

- Record breaking changes, deprecations, migrations, and platform differences.
- Never introduce a competing token namespace or component library without recording the incompatibility and migration path.
- Promote a pattern only after recurrence and a real consumer prove it.
- Keep product-specific components separate from generic primitives.

### Composability

For product screens, flows, and visual experience, compose with `design-engineering`. This skill owns the design system foundation, component contract, and safe evolution only.

## Validation

Use the cheapest checks that provide evidence:

- token lint or static scan for unapproved literals;
- typecheck and component tests;
- Storybook or component catalog for states and variants;
- accessible contract validation: semantic roles, focus management, contrast ratios, keyboard interaction at the component level;
- browser or native runtime validation for affected interactions.

If a check is unavailable, report it as not run. An isolated preview does not prove product support.

## Common mistakes

- creating a massive library before product needs exist;
- coupling semantic names to raw colors such as `blue-500`;
- allowing screen code to bypass component contracts;
- treating visual similarity as proof of behavior;
- adding a second styling system to avoid migrating the first;
- changing tokens or component APIs without a documented migration path.
