# Architecture-neutral scenario catalogue

These are task families, not executable study tasks. Concrete requirements, fixture values and hidden expectations must be independently authored and withheld from migration implementers until variants freeze. Every actual task specifies observable business goals, existing behavior to preserve, input/output and state invariants, error behavior, security and performance constraints. Do not prescribe interfaces, adapters, layer names, files or patterns.

| ID | Business objective | Change pressure |
| --- | --- | --- |
| T01 | Introduce a pricing/fee policy | Business-rule evolution |
| T02 | Replace a payment/integration provider | Dependency substitution |
| T03 | Support multiple providers | Concurrent integration variants |
| T04 | Add a jurisdiction-specific rule | Policy isolation |
| T05 | Prevent duplicate effects after retry | Idempotency |
| T06 | Recover from partial transaction failure | State consistency |
| T07 | Deliver notifications asynchronously | Communication boundaries |
| T08 | Support a new storage implementation | Persistence dependency |
| T09 | Introduce customer/account classification | Domain evolution |
| T10 | Produce an immutable audit record | Cross-cutting requirements |
| T11 | Require authorization or approval | Workflow and security |
| T12 | Remove a deprecated capability | Change/deletion propagation |
| N01 | Localized output formatting/default change | Negative control |

Pilot families: T01, T02, T06 and N01, subject to project qualification. Choose domain-appropriate equivalent goals and publish sampling rationale before execution. Include at least one pure behavior-preserving refactoring task in the expanded study, specified by an external operational goal (e.g. preserve all behavior while retiring a deprecated dependency). Analyze it separately from business evolution. Independent and cumulative modes answer different questions.

## Oracle

An independent, protected evaluator owns the business acceptance criteria. Baseline regressions must pass before any change; new tests must initially fail for the intended reason. Test through stable public contracts wherever feasible. Preserve existing output and persisted state, verify transactions with deterministic local dependencies, and exercise timeout, duplicate, rollback and denial paths. Include property/metamorphic checks where meaningful. A fake alone does not establish real persistence or protocol behavior.

Illustrative provider substitution: successful transaction produces exactly one ledger effect; decline does not complete purchase; historic references and refunds remain valid; timeout/retry does not duplicate payment; reconciliation totals match; public contract remains compatible; no sensitive data in logs. This example is not a frozen task or a claim of implemented tests.

Visible tests and hidden evaluation use equivalent semantics across arms. Independent oracle review and fault-detection checks guard against weak or implementation-coupled tests. Neither migration nor change agents may modify evaluator expectations, see hidden fixtures in advance, or certify their own results.

Tracking: #4 and #5.
