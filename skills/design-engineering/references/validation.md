# Validation, Hallucination Detection & Visual QA

## Why

Generative UI tools confidently invent features, metrics, and navigation. The failure mode is silent: output *looks* plausible, so violations slip in unless each requirement is traced to evidence. Validation is comparison against the Screen Spec, not aesthetic judgment.

## Stitch / generative tool rules

- Treat the tool as an optional **visual renderer**, never a product architect.
- Send one bounded design problem at a time: screen ID, purpose, layout with dimensions, required components, allowed interactions, design system tokens, visual direction, prohibited list.
- If the design system was configured in the tool (e.g. `create_design_system`/`update_design_system`), pin it so results share tokens.
- Read results back (`get_screen`) rather than assuming the call succeeded.

Hallucination signals → bypass the tool and implement directly:
- fabricates structure after correction (2–3 failed iterations)
- invents domain data the prompt forbids
- reference fidelity matters more than exploration

## Discrepancy taxonomy

| Code | Meaning |
|---|---|
| MISSING_REQUIRED_ELEMENT | Spec-required component/action/state absent |
| INVENTED_ELEMENT | Element not in spec (widgets, metrics, AI features, nav items, attributes) |
| STRUCTURAL_CHANGE | Layout/hierarchy contradicts spec |
| NAVIGATION_CHANGE | Added/removed/renamed navigation |
| BUSINESS_RULE_CHANGE | Roles, permissions, workflow or rule altered |
| TERMINOLOGY_CHANGE | Domain concept renamed/relabelled |
| DESIGN_SYSTEM_VIOLATION | Off-token color/type/spacing/component |
| ACCESSIBILITY_PROBLEM | Contrast, focus, labels, targets, semantics |
| RESPONSIVE_PROBLEM | Breakpoint behavior contradicts spec |
| LOW_VISUAL_QUALITY | Unprofessional rendering even if structurally right |
| IMPLEMENTATION_RISK | Engineering cannot reasonably build it |

## Validation report template

`design/validation/SCR-xxx-validation.md`:

```markdown
SCREEN: SCR-003
FIDELITY: PASS | FAIL | WAIVED | NOT RUN
ISSUES:
- [CRITICAL] INVENTED_ELEMENT: "Property Valuation" widget — not in spec.
- [HIGH] MISSING_REQUIRED_ELEMENT: Timeline action absent.
- [MEDIUM] DESIGN_SYSTEM_VIOLATION: sidebar 200px, spec says 240px.
ACTION: REGENERATE | CORRECT | ACCEPT
```

Severity guide: CRITICAL = invented/dropped requirement or business rule; HIGH = missing required element, nav/structure change; MEDIUM = design-system or responsive deviation; LOW = polish.

## Acceptance rules

Add a traceability table: `screen-spec requirement | evidence | PASS / FAIL / NOT RUN`.

- **PASS:** all required rows have evidence and no CRITICAL/HIGH issue remains.
- **FAIL:** a required row is missing, contradicted, or has an open CRITICAL/HIGH issue.
- **WAIVED:** a named owner records rationale, affected scope, and review point; it cannot silently change behavior, permissions, security, or policy.
- **NOT RUN:** evidence could not be collected; report why instead of implying a pass.

Approved design-system components/tokens and necessary semantic, focus, screen-reader, or platform plumbing are allowed when named in the Screen Spec. Unexpected product content, behavior, navigation, or information architecture remains an `INVENTED_ELEMENT`.

## Rejection loop

```
SPEC → GENERATE → INSPECT → CRITIQUE → CORRECT → REGENERATE → VALIDATE
```

Default limit: 3 iterations per screen. On repeated structural failure, stop and implement directly from the spec — do not keep re-prompting a tool that cannot hold the contract.

Never: PROMPT → GENERATE → ACCEPT.

## Visual QA (post-implementation)

When browser tools exist (e.g. `webapp-testing`):

1. Run the app; navigate to the screen under test.
2. Capture screenshots at every breakpoint required by the Screen Spec.
3. Compare against approved spec/screenshot/reference.
4. Record each discrepancy (taxonomy above) as a correction task.
5. Create correction tasks; apply source fixes only when authorized; re-capture and repeat until clean.

Checklist: spacing, alignment, typography, sizing, colors, hierarchy, missing components, incorrect components, overflow, interaction states (hover/focus/disabled/loading), responsive behavior, accessibility (tab order, focus rings, contrast, labels).
