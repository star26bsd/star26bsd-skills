# Related skills and prior art

This file records the “has someone already done this?” check. These skills contain useful pieces, but none inspected combined codebase evidence, contract ownership, tracer-slice readiness, YAGNI, and stop-and-rescope behavior for one proposed implementation unit.

Public skills evolve. Re-run discovery through [find-skills](https://github.com/vercel-labs/skills/blob/main/skills/find-skills/SKILL.md), [skills.sh](https://skills.sh/), and source search before publishing De-spoon externally.

## Primary inspiration: Matt Pocock's composable workflow

DMNG's skill workflow is heavily adapted from Matt Pocock's [Skills for Real Engineers](https://github.com/mattpocock/skills), which favors small, composable skills that preserve human control rather than one framework owning the whole process.

The relevant upstream flow is:

1. [`grill-me`](https://github.com/mattpocock/skills/blob/main/skills/productivity/grill-me/SKILL.md) and [`grill-with-docs`](https://github.com/mattpocock/skills/blob/main/skills/engineering/grill-with-docs/SKILL.md) align intent and domain language.
2. [`to-spec`](https://github.com/mattpocock/skills/blob/main/skills/engineering/to-spec/SKILL.md) turns the discussion into a specification while preferring existing test Seams.
3. [`to-tickets`](https://github.com/mattpocock/skills/blob/main/skills/engineering/to-tickets/SKILL.md) creates independently demonstrable tracer-bullet tickets with blocking edges.
4. [`implement`](https://github.com/mattpocock/skills/blob/main/skills/engineering/implement/SKILL.md) executes approved work through feedback loops.
5. [`improve-codebase-architecture`](https://github.com/mattpocock/skills/blob/main/skills/engineering/improve-codebase-architecture/SKILL.md) and its codebase-design vocabulary inform DMNG's Module, Interface, Seam, Adapter, depth, leverage, and locality language.

De-spoon preserves that workflow and fills a narrower gap exposed through use: even a meaningful spec and a nominally vertical ticket can still carry future architecture, duplicated contracts, or adjacent hardening into implementation. It adds a read-only scope pass between ticket creation and implementation; it does not replace or fork Matt Pocock's skills.

Adopted workflow principles include composability, codebase inspection before invention, domain-language continuity, tracer-bullet delivery, existing-Seam preference, human approval, and small deliberate feedback loops.

## Public skills inspected

### Story Refiner

- [skills.sh](https://skills.sh/gustavogutierrez/engineering-skills/story-refiner)
- [source](https://github.com/GustavoGutierrez/engineering-skills/blob/main/skills/story-refiner/SKILL.md)
- Adopt: INVEST, observable Given/When/Then criteria, explicit assumptions, splitting oversized stories, avoiding implementation leakage.
- Gap: not codebase-aware; does not distinguish existing contracts from new responsibility or test speculative internal machinery.

### User Story Review

- [source](https://github.com/majiayu000/claude-skill-registry/blob/main/skills/data/user-story-review/SKILL.md)
- Adopt: inspect current code/tests, compare current and requested behavior, identify mixed scope and developer risk.
- Gap: feedback-only; no INVEST/YAGNI/tracer verdict, contract classification, or tightened rewrite.

### Planning and Task Breakdown

- [skills.sh](https://skills.sh/addyosmani/agent-skills/planning-and-task-breakdown)
- [source](https://github.com/addyosmani/agent-skills/blob/main/skills/planning-and-task-breakdown/SKILL.md)
- Adopt: vertical slices, explicit verification, dependency awareness, working checkpoints.
- Reject: universal file-count limits and foundation-first layer ordering. A vertical slice may legitimately cross several file types and layers.

### Story Quality

- [skills.sh](https://skills.sh/rohunj/claude-build-workflow/story-quality)
- [source](https://github.com/rohunj/claude-build-workflow/blob/main/skills/story-quality/SKILL.md)
- Adopt: readiness verdict, specific acceptance feedback, dependency review.
- Reject: rules that discourage multiple file types and prescribe schema → API → UI stories; those rules create horizontal slices.

### YAGNI Principle

- [skills.sh](https://skills.sh/kayaman/skills/yagni-principle)
- [source](https://github.com/kayaman/skills/blob/main/yagni-principle/SKILL.md)
- Adopt: distinguish speculative capability from sound current design; require a confirmed current need; consider cost of build, delay, carry, and repair.
- Gap: evaluates code/design generally rather than whether one proposed delivery slice is ready.

### Ponytail

- [skills.sh](https://skills.sh/dietrichgebert/ponytail/ponytail)
- [source](https://github.com/DietrichGebert/ponytail/blob/main/skills/ponytail/SKILL.md)
- Adopt: inspect before inventing; reuse codebase/platform/dependencies before adding code; no scaffolding “for later.”
- Reject: shortest-diff incentives and an implementation persona can remove necessary completeness or conflate issue readiness with coding style.

### PM Scope

- [source](https://github.com/jay1803/ship-skills/blob/main/pm-scope/SKILL.md)
- Adopt: smallest coherent user/operator outcome; explicit in/out/deferred/dangerous areas; split when risk, ownership, dependency, or acceptance differs.
- Gap: product-scoping artifact without codebase contract verification or anti-framework analysis.

### Hamburger Method

- [skills.sh](https://skills.sh/eferro/augmented-lean-delivery/hamburger-method)
- [source](https://github.com/eferro/augmented-lean-delivery/blob/main/hamburger-method/SKILL.md)
- Adopt: compose a usable vertical slice across the full flow and consider simpler options at each layer.
- Reject: always generating many variants and treating omitted error handling as a default simplification; current safety determines completeness.

### ProductSpec

- [skills.sh](https://skills.sh/gokulrajaram/productspec/productspec)
- [source](https://github.com/gokulrajaram/ProductSpec/blob/main/skills/productspec/SKILL.md)
- Adopt: product intent as contract, explicit cuts/non-goals, acceptance traceability, no silent scope drift.
- Gap: governs spec conformance rather than determining whether one implementation unit contains speculative work.

## DMNG workflow neighbors

- `grill-with-docs` challenges and records product/domain decisions.
- `to-issues` converts approved plans into tracer-bullet issues.
- `improve-codebase-architecture` supplies Module, Interface, Seam, Adapter, depth, leverage, and locality language.
- `de-spoon` reviews one proposed implementation unit after planning and before execution.
- `pick-issue` implements a delivery slice only after it is ready.

De-spoon must not absorb the creation, architecture, or implementation workflows of these neighboring skills.

## Publication note

The current wording is an original synthesis. If future revisions copy templates or substantial wording from another skill, inspect and preserve that source’s license and attribution requirements before publication.
