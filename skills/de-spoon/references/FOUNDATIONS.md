# Foundations

De-spoon is a synthesis, not a new software-development theory. The Matrix metaphor is a memory aid; the review rules come from the established practices below.

## Evidence levels

| Level | Meaning |
|---|---|
| Empirical | Research observes measurable associations across organizations. It informs risk but does not prove every small change is better. |
| Industry practice | Durable practitioner method or heuristic with broad use. Apply with judgment rather than treating it as a law. |
| Practitioner guidance | Contemporary field experience that supplies useful working language or techniques, not scientific proof. |
| Formal design framework | A precise way to reason about responsibilities and guarantees. |
| Project policy | A concrete operational rule derived from the sources and DMNG experience. |

## Reading list at a glance

| Reference | Principle used by De-spoon |
|---|---|
| Thariq, “A Field Guide to Fable: Finding Your Unknowns” | Map versus territory; known knowns, known unknowns, unknown knowns, and unknown unknowns |
| Bill Wake, “INVEST in Good Stories and SMART Tasks” | Independent, valuable, small, testable implementation units |
| Alistair Cockburn, *Crystal Clear* | Walking Skeleton: a tiny real end-to-end function |
| Andrew Hunt and David Thomas, *The Pragmatic Programmer* | Tracer Bullets, deliberate small steps, fast feedback |
| Kent Beck, *Extreme Programming Explained* | YAGNI, simple design, continuous design investment |
| Agile Manifesto principles | Maximize work not done without abandoning technical excellence |
| Jez Humble and David Farley, *Continuous Delivery* | Independently deployable, reversible small batches |
| Nicole Forsgren, Jez Humble, and Gene Kim, *Accelerate* | Empirical basis for small-batch delivery and feedback |
| Dan North, “Introducing BDD” | Acceptance criteria as observable behavior |
| Gojko Adzic, *Specification by Example* | Concrete examples as shared, testable specification |
| Bertrand Meyer, *Object-Oriented Software Construction* / Design by Contract | Preconditions, postconditions, and invariants; assumptions versus owned responsibility |
| John Ousterhout, *A Philosophy of Software Design* | Deep Modules, small Interfaces, complexity hidden with locality |
| Eric Evans, *Domain-Driven Design* | Ubiquitous language and behavior owned by the appropriate domain model |
| Titus Winters, Tom Manshreck, and Hyrum Wright, *Software Engineering at Google* | Sustainable engineering and evidence-aware change at scale |
| Kent Beck, *Tidy First?* | Separate preparatory structure from behavior changes; make small reversible improvements |

The sections below provide links, evidence level, and the exact way each principle constrains the skill.

## Sources and what De-spoon borrows

### Map versus territory and unknowns — practitioner guidance

Thariq frames prompts, skills, plans, and context as the **map**, while the codebase and real-world constraints are the **territory**. Their difference produces four useful categories:

- **Known knowns:** explicit requirements and verified facts.
- **Known unknowns:** recognized unresolved questions.
- **Unknown knowns:** tacit knowledge or taste that becomes visible through examples, prototypes, references, or interviews.
- **Unknown unknowns:** blind spots that require proportionate exploration and can never be proven absent.

De-spoon uses this taxonomy before applying YAGNI. An unknown is not removable fat; speculative machinery invented to conceal or prematurely answer it is a spoon. The skill routes unknowns to grilling, prototypes, references, research, or a blocking decision rather than absorbing those workflows.

- Thariq, [A Field Guide to Fable: Finding Your Unknowns](https://x.com/trq212/status/2073100352921215386)
- Thariq, [Know your unknowns — examples](https://thariqs.github.io/html-effectiveness/unknowns/)

### INVEST — industry practice

Bill Wake introduced INVEST in 2003: Independent, Negotiable, Valuable, Estimable, Small, and Testable.

De-spoon uses INVEST to test whether proposed work is independently valuable and ready to verify. “Small” is contextual; it is not a universal file, line, hour, or story-point limit.

- Bill Wake, [INVEST in Good Stories and SMART Tasks](https://xp123.com/invest-in-good-stories-and-smart-tasks/)

### Walking Skeleton and Tracer Bullets — industry practice

A Walking Skeleton is a tiny end-to-end implementation that connects the important parts of a system. Tracer Bullet development creates a lean but real path through the final environment and grows it incrementally.

De-spoon uses these practices to reject horizontal slices that produce infrastructure without one demonstrable outcome.

- Alistair Cockburn, *Crystal Clear* (Walking Skeleton)
- Andrew Hunt and David Thomas, [*The Pragmatic Programmer*](https://pragprog.com/titles/tpp20/the-pragmatic-programmer-20th-anniversary-edition/) (Tracer Bullets)

### YAGNI and Simple Design — industry practice

Extreme Programming’s YAGNI rule says not to implement capability merely because it may be useful later. Martin Fowler distinguishes speculative capability from work that makes current code easier to modify.

De-spoon asks which current acceptance criterion requires every proposed mechanism. A future consumer alone is not proof.

- Kent Beck, *Extreme Programming Explained*
- Martin Fowler, [YAGNI](https://martinfowler.com/bliki/Yagni.html)

### Agile simplicity — industry principle

The Agile Manifesto calls simplicity “the art of maximizing the amount of work not done.” De-spoon applies this without weakening the completeness, safety, or demonstrability of the current outcome.

- [Principles behind the Agile Manifesto](https://agilemanifesto.org/principles.html)

### Small batches and Continuous Delivery — empirical research and industry practice

DORA research associates small batches with better software-delivery performance. Continuous Delivery explains why small, independently deployable changes shorten feedback loops and reduce release risk.

De-spoon therefore prefers independently deployable, reversible slices and treats unexpected subsystem growth as a stop-and-rescope signal. The research does not justify arbitrary file-count limits.

- DORA, [Working in small batches](https://dora.dev/capabilities/working-in-small-batches/)
- Nicole Forsgren, Jez Humble, and Gene Kim, *Accelerate*
- Jez Humble and David Farley, [*Continuous Delivery*](https://martinfowler.com/books/continuousDelivery.html)

### BDD and Specification by Example — industry practice

Behavior-Driven Development treats acceptance criteria as observable behavior. Specification by Example uses concrete examples to create a shared, testable understanding.

De-spoon uses this to move architectural aspirations out of acceptance criteria unless the current observable outcome requires them.

- Dan North, [Introducing BDD](https://dannorth.net/introducing-bdd/)
- Gojko Adzic, *Specification by Example*

### Design by Contract — formal design framework

Design by Contract distinguishes preconditions, postconditions, and invariants. De-spoon adapts that distinction:

- Existing contracts and verified dependencies are assumptions/preconditions.
- New behavior owned by the slice is its postcondition.
- Existing safety and domain guarantees are regressions/invariants.

- Bertrand Meyer, [Design by Contract](https://se.inf.ethz.ch/~meyer/publications/old/dbc_chapter.pdf)

### Deep Modules and locality — design framework

A deep Module hides substantial implementation behind a small Interface. Locality keeps related knowledge and change with its owner.

De-spoon prefers existing Modules and Interfaces. A new abstraction needs evidence from the current slice; reuse must not duplicate business rules outside their owning Module.

- John Ousterhout, *A Philosophy of Software Design*
- DMNG’s `improve-codebase-architecture` skill and its `LANGUAGE.md`

### Ubiquitous language — industry design practice

Domain-Driven Design uses a shared domain language to align conversation, documentation, and code. De-spoon uses the project's established vocabulary to identify the real outcome and owning Module instead of inventing parallel concepts.

- Eric Evans, [*Domain-Driven Design*](https://www.domainlanguage.com/ddd/)

### Sustainable and preparatory change — industry practice

*Software Engineering at Google* emphasizes software's evolution over time and the costs of scale and change. De-spoon applies that perspective by requiring evidence for generalized machinery rather than treating scale-oriented practices as automatic current requirements.

*Tidy First?* separates small structural preparation from behavior change. De-spoon permits preparatory work when it demonstrably makes the current slice safer or simpler; independently valuable cleanup remains a separate follow-up.

- Titus Winters, Tom Manshreck, and Hyrum Wright, [*Software Engineering at Google*](https://abseil.io/resources/swe-book)
- Kent Beck, *Tidy First?*

## DMNG policy derived from the sources

The following are local operating rules, not claims of universal science:

1. Give each criterion one primary class: new responsibility, verified assumption, regression, activation, follow-up, or unresolved unknown.
2. If an assumption can change implementation or acceptance, verify it before declaring the work ready.
3. If an assumption is false, stop and rescope; do not silently absorb the discovered work.
4. Name expected touchpoint categories, but do not impose universal file or line budgets.
5. New generic machinery requires a current acceptance behavior and evidence that existing Interfaces are insufficient.
6. Keep safety required by the current outcome. “Minimal” means smallest complete change, not fewest edits.

## The metaphor

“There is no spoon” represents the moment an apparently fixed requirement is recognized as an assumption. To **de-spoon** is to stop bending the real system around imagined needs. The metaphor helps recall the process; it is not the methodological authority behind it.
