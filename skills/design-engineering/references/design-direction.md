# Design Direction & Anti-Generic Rules

## Direction is domain-matched

Define deliberately per product before styling anything: visual personality, density, typography philosophy, spacing, borders, radius, elevation, iconography, imagery, motion, information hierarchy, light/dark strategy, responsive philosophy. The domain dictates the language:

- **GIS**: map-first, high information density, contextual panels, layered controls, spatial interaction, chrome recedes behind the map.
- **Healthcare**: clarity, trust, high readability, explicit status, low ambiguity, generous contrast.
- **Fintech**: numerical hierarchy, transactional clarity, explicit security states, strong data visualization, tabular numerals.
- **Dashboards/SaaS**: scannable KPI hierarchy, dense tables where the job is monitoring; resist decorative charts.
- **Developer tools**: terminal-adjacent density, monospace where appropriate, keyboard-first.
- **Consumer/social**: imagery-forward, motion as feedback, lower density.

Do not reuse one visual language across products.

## Anti-generic rules

AI-generated UI converges on a recognizable default. Avoid unless justified by the domain:

- excessive rounded cards; every section wrapped in a card
- giant hero gradients; purple/blue gradient abuse
- meaningless statistics, decorative charts, fake activity feeds, fake "AI insights"
- glassmorphism everywhere, random pills, unnecessary floating elements
- excessive whitespace that destroys information density for professional tools

Test every element: it must serve **information**, **action**, **hierarchy**, **feedback**, or **brand**. If it serves none, delete it.

Compose with the `frontend-design` skill when available for typography/aesthetic exploration — but the direction decisions recorded in `design/design-direction.md` remain the contract.
