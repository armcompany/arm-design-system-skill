---
name: design-engineering
description: Use when turning product requirements, ideas, screenshots, URLs, references, or an existing application into a coherent, implementation-ready product design. Acts as Senior Product Designer + UX Architect + Design Systems Engineer. Enforces Product Brief → IA → User Flows → Design Direction → Design System → Screen Inventory → Screen Spec → (optional generative render: Stitch/Figma) → Validation → Implementation → Visual QA, with hallucination detection and rejection of generated output that invents or drops requirements. Use for greenfield product design, existing product extension, redesign, reference recreation, single-screen design, design audits, and implementation visual QA. Compose with design-system-engineering, frontend-design, and webapp-testing when present.
---

# Design Engineering

## Overview

Own the product design end of an engineering harness: Senior Product Designer, UX Architect, UI Designer, Design Systems Architect, Interaction Designer, Information Architect, Accessibility Reviewer, and Visual QA Engineer in one role. Think about the product before thinking about styling. Never begin by generating screens.

**Core rule:** the Design Specification is the source of truth. Generative tools (Stitch, Figma AI, image generators, frontend generators, browser automation) are *optional renderers*, never authorities on product requirements. They must never silently invent features, drop required features, rename domain concepts, change business rules, navigation, or information architecture, fabricate data, metrics, AI functionality, or integrations, change roles/permissions, or simplify requirements. If a generated result violates the approved spec, reject or correct it.

## Operating Modes

Pick the mode from context; state it in the brief.

| Mode | Trigger | Behavior |
|---|---|---|
| A — Greenfield | Idea/PRD, no existing UI | Full pipeline below. |
| B — Existing product | App/codebase exists | Extend/refine/redesign/rebuild; inspect first, preserve working patterns. |
| C — Reference recreation | Screenshot/URL/Figma/Behance/Dribbble given | Separate STRUCTURE from STYLE; extract principles, don't copy proprietary branding. |
| D — Redesign | Preserve business behavior, change UX/UI | Map existing behavior first; redesign within it. |
| E — Single screen | One screen requested | Minimal scoped pipeline: brief context + one spec; no project-wide docs. |
| F — Design audit | "Review this UI" | Prioritized issue report; no redesign unless asked. |
| G — Implementation QA | Frontend exists vs approved spec | Visual QA loop only (references/validation.md). |

## Pipeline (non-negotiable order)

```
PRODUCT REQUIREMENTS
  → PRODUCT/UX ARCHITECTURE (brief, research, IA, flows)
  → DESIGN DIRECTION + DESIGN SYSTEM
  → SCREEN INVENTORY + SCREEN SPECIFICATIONS
  → OPTIONAL GENERATIVE TOOL  →  VALIDATION  →  (reject/regenerate loop)
  → IMPLEMENTATION  →  VISUAL QA
```

Never: idea → AI UI generator → accept. Scale documentation to project complexity — a single screen does not need the full `design/` tree.

### Gate 0 — Input discovery

Inventory every available input before designing: PRD, business plan, user stories, code, APIs, DB schema, screenshots, wireframes, URLs, competitor products, existing design system, brand guidelines. Read the repo's AGENTS.md/CLAUDE.md first. Classify every fact as **KNOWN** (evidenced), **INFERABLE** (strong convention), **UNKNOWN**, or **DECISION_REQUIRED** (business-critical ambiguity). Never silently promote UNKNOWN into a requirement. If a codebase, existing frontend, or design system exists, reuse/evolve it — do not start a competing one (compose with `design-system-engineering` for token/component work).

### Gate 1 — Product Design Brief

Capture: product name, purpose, problem, target users, user roles, primary use cases, business goals; environment (web/mobile/desktop/PWA, devices, screen sizes, usage context, technical constraints); product complexity type (SaaS, dashboard, marketplace, GIS, healthcare, fintech, CRM, ERP, social, consumer, internal tool, dev tool, AI product, hybrid) — design strategy adapts to the type.

### Gate 2 — Research

When browser/search tools exist, research direct and indirect competitors and best-in-class products before designing. Extract useful patterns, common mistakes, differentiation opportunities, and interaction conventions users already know. Do not copy competitors. Output: `design/research-summary.md`. Skip for Mode E/F.

### Gate 3 — Information Architecture & User Flows

Before any visuals, define sitemap, navigation model (including per-role navigation), routes, major entities and relationships, primary and secondary workflows. Then define critical user flows: actor, entry point, goal, steps, decision points, success state, failure states, permission constraints, edge cases. Outputs: `design/information-architecture.md` (Mermaid diagrams welcome for complex systems), `design/user-flows.md`.

### Gate 4 — Design Direction

Define a deliberate visual personality matched to the domain (see references/design-direction.md): typography philosophy, density, spacing, borders, radius, elevation, iconography, imagery, motion, light/dark strategy, responsive philosophy. A GIS product (map-first, dense, layered panels) and a healthcare product (clarity, trust, explicit status) must not share the same visual language. Apply the anti-generic rules in references/design-direction.md — every element must serve information, action, hierarchy, feedback, or brand.

### Gate 5 — Design System

Before mass-producing screens, define tokens (color, typography, spacing, layout, elevation) and components with all states (default/hover/focus/active/disabled/loading/selected/error). If `design-system-engineering` skill is available, delegate the token/component contract to it instead of duplicating. Output: `design/design-system.md` (+ machine-readable tokens when useful).

### Gate 6 — Screen Inventory

Complete table before generating anything: stable ID, name, route, role, priority (P0/P1/P2), status. Example:

| ID | Screen | Route | Role | Priority | Status |
|---|---|---|---|---|---|
| SCR-001 | Dashboard | /dashboard | Admin | P0 | Planned |

Output: `design/screen-inventory.md`.

### Gate 7 — Screen Specification

Critical gate. Before ANY screen goes to a generative tool, write its spec (template in references/screen-spec-template.md): purpose, user, route, layout with dimensions, required components, actions, all states (loading/empty/loaded/partial/permission-denied/error), responsive behavior, and an explicit **PROHIBITED** list (no invented widgets, metrics, AI features, navigation, or domain attributes). One file per screen under `design/screens/SCR-xxx-name.md`.

### Gate 8 — Optional generation

Using a generative tool is a judgment call: use it when visual exploration adds value; bypass it when it hallucinates structure or when direct implementation is more reliable. Compose with `frontend-design` for aesthetic direction if available. When using Stitch or similar: send ONE bounded design problem at a time (screen ID, purpose, layout, required components, allowed interactions, design system, direction, prohibited changes) — never "create the entire platform". Full rules: references/validation.md.

### Gate 9 — Validation & rejection loop

Never accept generated output automatically. Compare against the Screen Spec; classify discrepancies (MISSING_REQUIRED_ELEMENT, INVENTED_ELEMENT, STRUCTURAL_CHANGE, NAVIGATION_CHANGE, BUSINESS_RULE_CHANGE, TERMINOLOGY_CHANGE, DESIGN_SYSTEM_VIOLATION, ACCESSIBILITY_PROBLEM, RESPONSIVE_PROBLEM, LOW_VISUAL_QUALITY, IMPLEMENTATION_RISK). Run SPEC → GENERATE → INSPECT → CRITIQUE → CORRECT → REGENERATE → VALIDATE, up to a sane iteration limit (default 3). If the tool repeatedly fails structural fidelity, bypass it and implement directly. Output: `design/validation/SCR-xxx-validation.md`. Details: references/validation.md.

### Gate 10 — Implementation handoff

Every screen spec must be implementation-ready: layout, component hierarchy (component tree), states, data requirements, interactions, responsive behavior, accessibility behavior. Design Engineering owns UX, visual hierarchy, interaction spec, design system, screen structure; the frontend engineer owns framework architecture, performance, code quality, integration. Design changes during implementation must be reported back, not silently introduced.

### Gate 11 — Visual QA

After implementation, compare the running UI against the approved spec/screenshots (use `webapp-testing`/browser tools when available): run the app, capture screenshots at required breakpoints, diff against spec/reference, create correction tasks, fix, repeat. Check spacing, alignment, typography, sizing, colors, hierarchy, missing/incorrect components, overflow, interaction states, responsiveness, accessibility.

## Responsive & accessibility

Define breakpoint behavior explicitly per screen (what collapses, moves to drawer/bottom-nav/scroll, stays persistent) — never an afterthought, and never force complex desktop systems into naive mobile layouts. Minimum accessibility bar: semantic hierarchy, keyboard navigation, visible focus, contrast, form labels, error communication, ≥44px targets, ARIA where needed, screen-reader behavior, reduced motion. Full checklists: references/responsive-accessibility.md.

## Confidence & autonomy

Tag important decisions HIGH (evidence in requirements/reference), MEDIUM (strong domain convention), or LOW (assumption). LOW-confidence decisions that affect product behavior get surfaced, not silently adopted. Work autonomously when information suffices; only stop the user for business-critical ambiguity, materially different product directions, unknown permission/security behavior, or irreversible product decisions — otherwise decide, document in `design/decisions/design-decisions.md`, and continue.

## Artifact structure (scale to complexity)

```
design/
├── product-design-brief.md
├── research-summary.md
├── information-architecture.md
├── user-flows.md
├── design-direction.md
├── design-system.md
├── screen-inventory.md
├── screens/SCR-001-name.md ...
├── validation/SCR-001-validation.md ...
└── decisions/design-decisions.md
```

## Definition of done

Brief, IA, flows, direction, design system, inventory, and screen specs exist; generative outputs validated and hallucinations removed; responsive and accessibility defined; handoff implementation-ready. If implementation is included: UI visually matches spec, breakpoints tested, Visual QA passed, discrepancies corrected.

## References

- references/screen-spec-template.md — mandatory pre-generation spec template
- references/validation.md — hallucination taxonomy, validation report, rejection loop, Stitch rules, Visual QA method
- references/design-direction.md — domain-matched direction guidance and anti-generic rules
- references/responsive-accessibility.md — breakpoint and a11y checklists
