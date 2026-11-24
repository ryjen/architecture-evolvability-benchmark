# Measurement contract (draft)

The primary outcome is engineering cost to deliver independently accepted business behavior. Architectural appearance is not a success criterion.

## Trial result

Acceptance requires new requirements plus regression, contract, security and applicable performance gates, with exact candidate evidence. Set thresholds before trials. Record status: accepted, failed, timed_out, infrastructure_error, invalid_protocol, or not_started. Keep every scheduled trial; infrastructure failures require a preregistered disposition, not silent deletion or retries. Candidate failure is distinct from harness failure.

Pilot primary resource axis: wall-clock seconds from task release to independent acceptance, including required review and rework. Use a common wall-time ceiling and separate token/compute ceilings; record each actual value. If a secondary ceiling ends a trial before wall-time expiry, classify it as unsuccessful and apply the same predeclared wall-time penalty. Freeze numeric caps and review timing rules before starting; until then no trials are authorized by the protocol.

Primary joint outcomes:
1. Acceptance rate by fixed cap (accepted / eligible scheduled trials, with all statuses and exclusions separately reported).
2. Capped cost-to-acceptance: for an accepted trial, measured cost; for an eligible unsuccessful trial, predeclared cap in the relevant cost unit. This is a bounded penalty/estimand, not actual expenditure. Separately report actual consumed resources and sensitivity to penalty/cap. Report all scheduled trials by arm alongside eligible-trial estimates; not_started due to failed migration must not disappear from feasibility reporting. Time-to-event analysis may treat unresolved attempts as censored when assumptions are justified.

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

## Structural baseline procedure (proposed, not yet executed)

Use existing tools. Do not add a custom parser, analysis service, CI pipeline or hosted metrics account. Qualify and pin the tool versions and artifact digests before execution; source documentation alone is not a qualification receipt.

| Metric | Proposed collector | Definition and limits |
| --- | --- | --- |
| Production SLOC | [cloc](https://github.com/AlDanial/cloc) | Physical non-comment/nonblank Java source lines; separate other production languages and configuration. |
| Coupling and complexity | [CK](https://github.com/mauricioaniche/ck) | Tool-defined CBO, modified CBO, fan-in/out, WMC and method complexity. Record binding resolution and unresolved inputs; these are source metrics, not injected-field counts. |
| Cohesion | CK LCOM*, TCC, LCC; [jPeek](https://github.com/cqfn/jpeek) hitz95 LCOM4 | CK LCOM* and jPeek LCOM4 are distinct measures; no relabeling or conversion. LCOM4 requires compatible compiled classes and collector semantics. Preserve raw values and tool-specific treatment of constructors, statics, inherited fields and synthetic members. |
| Static dependency graph | [JDK 17 jdeps](https://docs.oracle.com/en/java/javase/17/docs/specs/man/jdeps.html) | Class-level direct references from compiled production outputs, all modules and resolved classpath, using -verbose:class -filter:none and nonrecursive analysis. Not a runtime call graph or full DI graph. |
| Cycles and reachability | Established directed-graph algorithms, e.g. [NetworkX SCC](https://networkx.org/documentation/stable/reference/algorithms/generated/networkx.algorithms.components.strongly_connected_components.html) | Reuse existing approved graph tooling if available; only a thin transformation/aggregation if unavoidable. No new graph framework. |

### Scope and reproducibility

For pinned Shopizer source, enumerate tracked production files under each of the five Maven modules' src/main trees. Use actual build source sets if they differ; exclude generated, vendored, test, example and build-output files from production source counts, with explicit path-level reasons. Retain resource/configuration inventory separately because Spring wiring affects dependency behavior. Create a deterministic sorted input manifest and hash it. Analyze all in-scope production Java files together to avoid hiding cross-module relationships. Retain raw collector outputs, command/argument versions, exit status, input hashes, diagnostics, resource use and tool artifact identities. Compare all variants with identical collector configuration and comparable scope rules, not identical file names.

For bytecode metrics include all production class outputs and complete dependency classpath; retain the mapping from source files to emitted classes. Define treatment of inner, anonymous and compiler-generated classes consistently; record excluded and unresolved edges. Report whole-project and module views plus a reviewed fixed business-capability mapping (checkout, payment, order totals, inventory, invoicing); the mapping follows capabilities after refactoring, not only their old package names. Report class counts and coverage with metric distributions (median, interquartile range, p90, maximum and denominator), and preserve outliers. Avoid relying on a project-wide mean when domain classes and DTOs dominate the population.

### Graph contract

Let V be all in-scope production class nodes, including isolated classes, and directed edge A -> B mean A statically depends on B. Deduplicate edges and exclude self-edges from direct graph statistics. Keep external dependencies in a separate inventory; graph reachability uses only internal nodes. Report incoming/outgoing degree, strongly connected components with at least two nodes, class count in cyclic components, largest component and cross-module edges. For an edge between an interface and its implementation, do not invent the reverse edge; model verified composition/wiring in a separate augmented graph and identify evidence for each added relation.

Propagation cost (PC) is the fraction of ordered node pairs reachable by zero or more directed edges, including the diagonal: PC = sum over v of (1 + number of distinct other nodes reachable from v) / |V|^2. Report N, numerator, denominator and a diagonal-excluded sensitivity measure when N > 1. For N = 0 report undefined. Reverse reachability measures potential dependents of a changed class, not guaranteed change effort. Report distributions of affected dependents. Apply the same convention to class and module graphs, reporting each separately. This follows the design-structure-matrix approach of [MacCormack, Rusnak and Baldwin (2006)](https://doi.org/10.1287/mnsc.1060.0552), with explicit benchmark conventions. Class splitting can change denominators; capability-level comparison and business outcomes are therefore necessary.

Qualify graph processing with fixtures: 3 isolated nodes -> PC 3/9, no cyclic SCC; A -> B -> C -> PC 6/9, no cyclic SCC; A <-> B with isolated C -> PC 5/9, one cyclic SCC of size 2. Verify distinct reachability (not path counts), isolated node retention and duplicate-edge handling. Qualify cohesion collector with small known one- and two-component examples according to its documented method inclusion rules. Report parser coverage and missing values; never interpret failure to resolve a dependency as zero coupling.

### Admission decision (review before collection)

For the medium pilot, proposed screening requirements: at least two stateful business workflows, at least three distinct external integration categories with verified wiring or executable contracts, and at least one representative business workflow with evidence of responsibility concentration and cross-capability coupling. Prefer upper-quartile CBO and LCOM4 greater than one in sampled business-service classes as supporting signals, not universal quality thresholds; report comparison population, exact selection rule and counterexamples. These provisional criteria were proposed after limited source screening, not before all candidate knowledge; that selection limitation must be recorded. Freeze the full-tree sampling and decision rules independently before collection and do not tune them using treatment outcomes. No single metric can establish low cohesion or treatment suitability.

### Collection gate

Run only in a qualified disposable environment with pinned tools, reviewed dependency resolution, no production credentials, restricted egress and bounded resources. Perform source-only cloc/CK first; then build and collect jdeps/jPeek after approval of the isolated execution environment. Record baseline build/test status separately. A missing collector or incomplete tree/build is a blocked or partial measurement, not a pass. No collector has been executed on Shopizer yet. Issue #3 remains open until the admission record is complete.

## Run record fields

Study/protocol revision; run ID; project/upstream SHA; arm and frozen starting SHA; task ID/hash; repetition; randomization seed/order; toolchain/environment/fixture hashes; model/harness identity and settings; limits; start/end and resource usage; candidate SHA; test oracle revision and outcomes; exact status and failure reason; cost breakdown; evidence references; reviewer disposition; protocol deviations. Never retain raw secrets or hidden tests in public records.

## Migration and economic analysis

For arm a after n changes: cumulative cost C_a(n) = M_a + sum(E_a,i), where M includes all arm-specific migration, review, equivalence testing and failed attempts; E includes accepted-change work and rework. Keep cost units explicit. Compare observed cumulative workloads, not just average successful trials. Independent trial sums are scenario-mix projections, not observed longitudinal costs. A failed change incurs actual cost without delivering a goal; cumulative sequences stop or follow a predeclared recovery rule. Report cost and number of accepted goals together; do not claim break-even from cheaper failure or unequal delivered outcomes. Report break-even if achieved; otherwise report not observed, with assumptions for sensitivity projections. Separate time, compute and monetary analyses; avoid double counting. Shared baseline/oracle costs are reported separately.

Tracking: #2 analysis freeze; #7 collection; #8 results.
