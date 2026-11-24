# Measurement contract (draft)

The primary outcome is engineering cost to deliver independently accepted business behavior. Architectural appearance is not a success criterion.

## Trial result

Acceptance requires new requirements plus regression, contract, security and applicable performance gates, with exact candidate evidence. Set thresholds before trials. Record status: accepted, failed, timed_out, infrastructure_error, invalid_protocol, or not_started. Keep every scheduled trial; infrastructure failures require a preregistered disposition, not silent deletion or retries. Candidate failure is distinct from harness failure.

Primary joint outcomes:
1. Acceptance rate by fixed cap (accepted / eligible scheduled trials, with all statuses and exclusions separately reported).
2. Capped cost-to-acceptance: for an accepted trial, measured cost; for an eligible unsuccessful trial, predeclared cap in the relevant cost unit. This is a bounded penalty/estimand, not actual expenditure. Separately report actual consumed resources and sensitivity to penalty/cap. Time-to-event analysis may treat unresolved attempts as censored when assumptions are justified.

Do not use a composite score that allows security failures to be offset by faster completion. If gates fail, not accepted.

## Metrics and units

| Dimension | Measure | Unit / collection |
| --- | --- | --- |
| Delivery | elapsed and active engineering time | seconds; monotonic clock, active intervals; human vs agent separately |
| Cost | tokens in/out/cache, inference spend, compute, human review | counts, currency + rate/date, CPU/wall seconds; no invented monetary rates |
| Refactoring | preparation, behavior-preserving restructuring, feature change, debugging and verification | categorized elapsed/active intervals with mixed/unknown bucket; independently sample classifications |
| Rework | rejected attempts and regression fixes | count and time; avoid double-counting overlapping phases |
| Correctness | accepted criteria, regression failures, invariant/contract failures | test identifiers and counts; frozen oracle |
| Test effort | authoring and maintenance time; fixture/setup burden; test execution duration | seconds, dependencies, changed tests; distinguish unit vs real integration |
| Assurance | mutation detection, flakiness, property and fault scenario results | tool/version, numerator and denominator; equivalent semantic fault sets where possible |
| Performance | latency, throughput, memory | defined workload, warmup, repetitions, environment; baseline deltas |
| Structure | CBO, LCOM4, cycles, propagation cost, complexity, duplication, change amplification | tool-specific definitions and fixed exclusions; explanatory only |
| Agent efficiency | tool calls, files read, context tokens, patch attempts | counts with collector limitations and redaction |

Count agent-generated test authoring and review in arm-specific delivery cost. Record independent oracle creation as common experiment cost; any architecture-specific compatibility work is arm-specific. Do not use LOC as a proxy for hours. Avoid asking an agent to estimate its own refactor effort without observed evidence. Report missing metrics as unknown.

## Run record fields

Study/protocol revision; run ID; project/upstream SHA; arm and frozen starting SHA; task ID/hash; repetition; randomization seed/order; toolchain/environment/fixture hashes; model/harness identity and settings; limits; start/end and resource usage; candidate SHA; test oracle revision and outcomes; exact status and failure reason; cost breakdown; evidence references; reviewer disposition; protocol deviations. Never retain raw secrets or hidden tests in public records.

## Migration and economic analysis

For arm a after n changes: cumulative cost C_a(n) = M_a + sum(E_a,i), where M includes all arm-specific migration, review, equivalence testing and failed attempts; E includes accepted-change work and rework. Keep cost units explicit. Compare observed cumulative workloads, not just average successful trials. Report break-even if achieved; otherwise report not observed, with assumptions for sensitivity projections. Separate time, compute and monetary analyses; avoid double counting. Shared baseline/oracle costs are reported separately.

Tracking: #2 analysis freeze; #7 collection; #8 results.
