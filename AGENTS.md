# AI Product Design Studio — Mandatory Agent Contract

You are working in an **executable product-specification workspace**, not a static design mockup. The human proposes ideas, tries candidate interactions, writes feedback, and approves outcomes. You own the tedious specification/implementation work within the guardrails below.

## Non-negotiable boundaries

1. **Preserve feature identity**. Every feature has an ID, user problem, goal, requirements, UI-facing fields, interaction variants, step scenarios and acceptance criteria. Register these in `src/data/features.js` (later versions may migrate to feature-local manifests).
2. **Never hardcode colors inside feature or component CSS**. Define new semantic tokens in `src/styles/tokens.css`, then reference them with `var(--token-name)`. Avoid ad-hoc font, spacing and motion values; prefer existing system scales.
3. **No silent rewrites of approved variants**. Create a candidate variant or Git branch. Existing variants must remain runnable until the reviewer approves a replacement.
4. **Never fabricate backend support**. Prototype field contracts are UI models, not evidence that a live business API supports them. Label mocked operations honestly.
5. **Keep runtime-independent prototypes**. A single demo component must be mountable with isolated state, be resettable, support deterministic `setStep(index)` and `replay(onStep)`, and expose `destroy()` to stop active timers.
6. **All changes must pass `npm run check`**. If interacting with code for which browser tests exist, run those tests too. Summarize what changed and which files or public components were affected.
7. **Prefer reuse over duplication**. Use design tokens and shared components; do not generate a new copy of the whole app for a minor variant.
8. **Keep humans in control**. AI can propose and implement candidate designs, but must not mark them approved on behalf of the human.
9. **Privacy first**. Browser localStorage is a demo store only. Never imply it is a secure cloud database or a backup mechanism.

## Feature workflow

1. Analyze request into problem, goal, out-of-scope and provisional assumptions.
2. Create or update feature metadata and UI-facing business field contract.
3. Model at least one happy path and one failure/alternate condition.
4. Implement one or more independently testable prototype variants.
5. Write/extend validation and interaction tests. Preserve the approved baseline.
6. Run checks, hand over a link to the live demo and summarize consequences.
7. Wait for human review. Only then record approval and prepare production integration work.

## Source map

- `src/data/features.js`: machine-readable feature and flow manifests
- `src/components/*.js`: isolated runnable prototypes (currently demo registry in `src/app.js`)
- `src/styles/tokens.css`: semantic token source of truth
- `src/styles/components.css`: shared styles referencing tokens
- `src/lib/validate.js`: structural requirements
- `scripts/check-design.mjs`: forbidden hardcoded color guardrail
- `tests/`: automated checks
- `docs/`: rationale, workflow, architecture and roadmap

## Change report format

Feature ID; requirement changes; field changes; prototype/interaction changes; design token changes; tests performed; known limitations; human decision requested.