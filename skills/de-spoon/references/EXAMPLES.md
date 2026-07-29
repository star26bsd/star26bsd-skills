# De-spoon examples

Use these examples to calibrate judgment. They illustrate the rubric; they are not templates that every work item must copy.

## 1. Broad scheduler becomes one delivery slice

### Proposed work

> Build a shared scheduler for integration jobs with a second policy registry, generic notification ordering, stale-job recovery, reconciliation, and all current/future producers.

### Reality map

- **New responsibility:** one protected scheduled tick must enqueue bounded payment checks and execute existing due jobs.
- **Existing contracts:** job ledger, claim function, handler registry, handler finalization, retry evidence.
- **Unknowns:** whether due selection and enqueue can be atomic through existing database Interfaces.
- **Spoons:** second registry, generic notification framework, stale recovery, reaction reconciliation, future producers.

### Tightened work

> Add one protected scheduled-tick route to the existing worker. Reuse the existing claim and handler path, add one bounded payment producer and one disabled Cron template. Permit one focused atomic producer RPC only if existing Interfaces cannot provide atomic selection/enqueue.

The removed items may be valuable. They are follow-ups because the current observable outcome does not exercise them.

## 2. Existing behavior is an assumption, not new scope

### Overloaded acceptance criteria

- The new scheduled invitation producer discovers due candidates.
- Invitation eligibility is correct for every lifecycle state.
- Access creation is atomic.
- Signed links never enter durable evidence.
- Mail retries and ambiguous outcomes are safe.
- Trial-date acknowledgements and withdrawal messages send automatically.

### Classification

| Criterion | Class | Action |
|---|---|---|
| Discover due candidates through the scheduler | NEW | Keep and test through the producer Interface. |
| Eligibility for every lifecycle state | ASSUMPTION | Cite the verified Selection Module contract and keep its existing regressions green. |
| Atomic access creation | ASSUMPTION | Cite the verified enqueue Interface; do not redesign it. |
| Credential-safe delivery evidence | ASSUMPTION | Cite the verified Delivery Adapter contract and keep its regressions green. |
| Retry and ambiguous-delivery behavior | ASSUMPTION | Do not change unless inspection shows the new connection violates the existing contract. |
| Acknowledgement and withdrawal delivery | ASSUMPTION | Verify existing events enqueue jobs and the generic tick executes due jobs; add no new producer. |

The new tests cover registration and delegation. They do not duplicate the dependency Modules’ full matrices.

## 3. Horizontal tasks become a tracer slice

### Horizontal split

1. Create all database tables.
2. Create all endpoints.
3. Create all screens.
4. Connect and test everything.

No early item is independently valuable or demonstrable.

### Vertical split

1. One authorized operator can create one valid record through the UI and see the persisted result.
2. The operator can edit that record.
3. The operator can archive and restore it.

Each slice may cross database, API, UI, and tests. Crossing layers is expected; producing only one layer is the warning.

## 4. Minimal does not mean unsafe

### Proposed cuts

- Remove authorization because it adds files.
- Skip idempotency because only one request is expected.
- Omit transactionality because the happy path works.
- Ignore keyboard access until a later polish issue.

These are not valid YAGNI cuts when the current outcome includes protected mutation, replayable side effects, atomic state, or an interactive UI. Security, data integrity, and accessibility are part of a complete outcome when currently applicable.

A spoon is unsupported future capability—not inconvenient present correctness.

## 5. Unexpected touchpoints are a stop signal

### Expected change shape

- Register one producer in the existing worker.
- Add one small Adapter and focused tests.
- Update existing operations documentation.
- No database, provider, or customer-copy change expected.

### Discovery during planning

The implementer concludes that three new database functions, a second runtime registry, and changes to customer mail payloads are necessary.

Do not silently proceed. One of these is true:

1. An existing assumption is false and the work is `BLOCKED`.
2. The proposed implementation is bending the system around a spoon.
3. The observable outcome was broader than stated and needs `RESLICE`.

Expected touchpoints are a reasoning aid, not a numeric budget. One legitimate cross-cutting change may touch many files; one unnecessary abstraction may touch only two.

## 6. Example review output

```markdown
## Verdict
TIGHTEN — the current outcome is valid, but three criteria require future-only machinery.

## Observable outcome
A verified customer receives one automatically scheduled invitation after the configured delay.

## Unknowns pass
| Unknown | Type | Evidence | Route | Blocking? |
|---|---|---|---|---|
| Does the existing Selection Module expose bounded due discovery? | Known known | Interface and focused tests inspected | Rely on the verified contract | No |
| Which candidates and due jobs exist at activation time? | Known unknown | Available only from production dry-run evidence | Require HITL dry-run before activation | Activation only |

## Reality map
- New responsibility: connect due discovery to the existing scheduled-producer Interface.
- Existing contracts: eligibility, access preparation, durable intent, signed delivery, generic job execution.
- Unknowns: none after code/test inspection.
- Spoons: generic invitation policy registry, new delivery finalizer, duplicated eligibility matrix.

## Change shape
- Expected touchpoint categories: one producer Module/test, existing worker registration/test, existing operations docs.
- Stop and rescope if: new SQL, handler payload, delivery semantics, or checkpoint behavior appears necessary.

## Acceptance review
| Criterion | Class | Keep/change/remove | Reason |
|---|---|---|---|
| Disabled by default | ACTIVATION | Keep | This producer owns its rollout gate. |
| Preview performs no writes | NEW | Keep | Observable producer contract. |
| Every lifecycle exclusion is implemented | ASSUMPTION | Change | The verified Selection Module owns it; keep its regressions green. |
| Add generic policy registry | FOLLOW-UP | Remove | No current behavior requires it. |

## Resulting work or unblock requirement
Add one disabled producer that delegates preview/enqueue to the existing Selection Module and returns the scheduler’s existing aggregate result. The existing generic tick executes the existing job. No SQL, handler, mail, or checkpoint changes.
```
