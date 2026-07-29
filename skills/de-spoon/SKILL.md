---
name: de-spoon
description: Reviews and tightens proposed implementation work before coding by separating current responsibility from existing contracts, false assumptions, and speculative machinery. Use after planning and before implementation to de-spoon an issue, ticket, story, or other work item into one complete, safe, independently demonstrable delivery slice.
license: MIT
---

# De-spoon

> There is no spoon. Build only what is real.

A **delivery slice** is a proposed unit of implementation work that produces one independently demonstrable outcome. The proposal is the **map**; the codebase and real constraints are the **territory**. An unknown is not fat. A **spoon** is guessed work used to hide or prematurely resolve an unknown, or justified only by duplicated responsibility or a hypothetical future consumer. De-spooning removes spoons while preserving the smallest complete current outcome.

This is a read-only pre-implementation review by default. Do not implement code or edit the tracker until the user approves the proposed rewrite.

## Grounding

The composable workflow and its position between ticket creation and implementation are directly inspired by [Matt Pocock's engineering skills](references/RELATED-SKILLS.md): grill and document → specify → create tracer-bullet tickets → implement. De-spoon adds a focused scope pass before implementation.

The rubric combines Thariq's map-versus-territory unknowns pass, INVEST, Walking Skeleton/Tracer Bullet development, YAGNI, Agile simplicity, small-batch delivery, BDD, Design by Contract, and deep Modules. See [foundations](references/FOUNDATIONS.md) when explaining why a rule exists and [related skills](references/RELATED-SKILLS.md) for prior art.

## Workflow

1. Read the proposed work, its governing PRD/ADR/plan, dependencies, and relevant repository instructions.
2. Inspect the current code and tests. Verify named Modules, Interfaces, Seams, Adapters, and assumed behavior rather than trusting the proposal.
3. State one observable user/operator outcome in one sentence. If there is more than one independent outcome, recommend reslicing.
4. Run an unknowns pass:
   - **Known knowns** — explicit, verified requirements or repository facts.
   - **Known unknowns** — recognized unresolved decisions; ask, decide, defer, or block.
   - **Unknown knowns** — tacit preferences recognized when seen; route to grilling, a prototype, or a reference.
   - **Unknown unknowns** — plausible blind spots; run proportionate codebase/research exploration. Never claim they are impossible.
5. Route unknowns instead of guessing. De-spoon does not conduct every interview, prototype, or investigation; material unresolved unknowns produce `BLOCKED`.
6. Build the reality map: **new responsibility**, **existing contracts**, **unknowns**, and **spoons**.
7. Give every criterion one primary class: `NEW` (owned behavior), `ASSUMPTION` (verified dependency), `REGRESSION` (existing invariant touched), `ACTIVATION` (rollout gate), `FOLLOW-UP` (separate value), or `UNKNOWN` (unresolved behavior/ownership).
8. Apply the tests and issue one verdict. For `READY`, `TIGHTEN`, or `RESLICE`, propose the resulting work; for `BLOCKED`, state the decision or evidence needed instead of guessing. Modify the original only after explicit approval.

## Tests

- **INVEST:** Is the work independent, negotiable, valuable, estimable, small, and testable?
- **Walking slice:** Does it produce one real end-to-end outcome rather than one horizontal layer?
- **Necessity:** Which current criterion requires each proposed abstraction, table, registry, policy, or framework?
- **Contract ownership:** Are existing guarantees stated as assumptions/regressions instead of new implementation?
- **Observable acceptance:** Do criteria describe externally observable behavior rather than architectural completeness?
- **Small batch:** Can it deploy, verify, disable, and roll back independently?
- **Change shape:** Do likely touchpoint categories match the outcome? Never impose a universal file/line limit.

## Spoon Signals

Treat these as prompts for proof, not automatic failures:

- “generic”, “all handlers”, “future”, “extensible”, “centralized”, “framework”, or “while we are here”
- A second registry, queue, policy layer, or abstraction—or machinery supporting every side of an unresolved decision
- Recovery, reconciliation, ordering, observability, or hardening not exercised by the current outcome
- Acceptance criteria that restate behavior already owned and tested elsewhere
- New database/provider/domain surfaces not implied by the observable outcome
- Tests that duplicate a dependency's full matrix instead of testing the new connection
- An unexpected subsystem or touchpoint category discovered during implementation planning

Security, privacy, data integrity, accessibility, idempotency, and required failure handling are not fat when the current outcome depends on them. Seek the smallest **complete** change, not the smallest diff.

## Verdicts

- **READY** — one complete slice; contracts are verified; known unknowns are resolved/routed; a proportionate blind-spot pass found no material blocker.
- **TIGHTEN** — the outcome is sound, but unknowns were prematurely answered with speculative machinery.
- **RESLICE** — an unknown reveals multiple outcomes, or horizontal/unfinished sibling work prevents independent value.
- **BLOCKED** — an unresolved unknown or false assumption can change implementation or acceptance.

## Output

```markdown
## Verdict
READY | TIGHTEN | RESLICE | BLOCKED — one-sentence reason

## Observable outcome
<One sentence>

## Unknowns pass
| Unknown | Type | Evidence | Route | Blocking? |

## Reality map
- New responsibility: ...
- Existing contracts: ...
- Unknowns: ...
- Spoons: ...

## Change shape
- Expected touchpoint categories: ...
- Stop and rescope if: ...

## Acceptance review
| Criterion | Class | Keep/change/remove | Reason |

## Resulting work or unblock requirement
<READY/TIGHTEN/RESLICE: proposed work; BLOCKED: decision or evidence needed>
```

Read [examples](references/EXAMPLES.md) when a slice is difficult to classify or tighten.
