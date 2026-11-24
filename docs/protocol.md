# Experimental protocol (draft v0.1)

Status: proposed, not preregistered or independently reviewed. Freeze a reviewed commit and analysis plan before confirmatory data collection. Pilot results are exploratory and cannot retrospectively establish confirmatory hypotheses.

## Questions and hypotheses

H1: Clean/SOLID (C) reduces cost-to-accepted-change compared with conventional refinement (B).
H2: C reduces regression repair and test development effort compared with B.
H3: benefits vary by change type, particularly business-policy and integration changes versus localized negative controls.
H4: cumulative savings may offset architectural migration cost; the break-even point may not exist.
H5: architecture may affect AI-assisted development cost and correctness.

Null or adverse outcomes are legitimate. Compare C versus A and B versus A as secondary contrasts. A bundled treatment cannot identify individual SOLID effects. Human developer comparisons require a separate controlled protocol; AI-only trials do not establish human productivity.

## Experimental arms

Freeze common baseline S0 after any necessary shared compatibility or fixture work. Report that preparation separately.

| Arm | Treatment |
| --- | --- |
| A | Original architecture; local refactoring and normal implementation techniques allowed. No initial migration. |
| B | Conventional behavior-preserving cohesion, deduplication and modularity improvements; no prescribed dependency rule. |
| C | Behavior-preserving Clean Architecture and SOLID transformation: inward source dependencies, cohesive business policies, consumer-owned ports at meaningful side-effect boundaries, explicit composition. |

B must not be intentionally weakened or prohibited from independently discovering useful SOLID practices. Record overlap and treatment separation; if distinction disappears, report it rather than forcing artificial degradation. Use equal, predeclared migration resource ceilings for B/C and include actual costs; stop when the ceiling is reached, not when a preferred structural score is achieved. Keep treatment instructions and review criteria versioned. Both arms may improve internal tests; count these as migration cost and retain them in subsequent trials. The external oracle is identical. Report differences in test investment as a potential mediator rather than silently equalizing away architectural effects. No gratuitous interfaces or wholesale rewrites without justification. Freeze variant snapshots after independent architecture review and equivalent regression/contract/invariant tests. Record any material differences in baseline performance. A failed migration is a study outcome, not an excluded arm. Mark its dependent trials not_started, report the arm as unavailable and do not manufacture a cost comparison against a nonexistent variant. A single migrated snapshot per arm does not separate architecture from migration implementer skill; later replication should independently construct multiple variants per arm or explicitly limit claims to the selected snapshots.

Task authors and oracle maintainers must not reveal concrete future requirements to migration implementers. Public catalogue is broad; independently authored concrete tasks and expected outcomes are held separately and identified by immutable hashes. Freeze task sampling and arm qualification before revealing tasks. Log access and any contamination. The public task-family catalogue provides general foreknowledge; concrete tasks alone are withheld. Treat this as a limitation and include an independently sampled unseen family in a later confirmatory study. Use separate fresh migration sessions with no access to experimental task artifacts or prior discussions.

## Experimental units and design

A trial is an isolated attempt at one project/task/arm under one pinned execution configuration. Independent mode resets to the qualified arm snapshot before each task; cumulative mode follows a frozen order and retains changes. Do not reuse a patch or agent memory between arms.

Pilot: one qualified medium subject, four task families including a negative control, three arms, three repetitions = 36 scheduled independent trials. Randomize order within project/task blocks with recorded seed. Counterbalance sequences for later cumulative runs. Model identity, tool permissions, time/token caps, resources, visible requirements, test opportunities and environment are held constant. Use fresh sessions; log actual rather than claimed model identity. If a model cannot be pinned, disclose the limitation and block confirmatory comparison or stratify versions prospectively.

Treat project and task as clusters; repetitions estimate within-task stochastic variability, not independent projects. One project per size cannot identify causal size effects. Determine expanded sample size and budget from pilot variance and feasibility; do not interpret a small pilot as definitive.

## Outcomes and analysis

Primary: acceptance probability by equal predeclared resource cap and capped cost-to-acceptance (all trials included; see measurement contract). Report both together; cheap failures are not successes. Secondary: successful-trial cost (selection-sensitive), refactoring/test effort, regression incidence, repair, performance and structural measurements. Use paired project/task blocks, report effect sizes and uncertainty with cluster-aware analysis where feasible; pilot reports descriptive matched comparisons, not unsupported population inference. Report distributions, missingness, ceiling effects and all failures. Set a practical minimum effect and non-inferiority gates before confirmatory work; no post hoc thresholds.

Include migration costs, failed migration attempts and cumulative cost sensitivity across change mixes. Separate shared study infrastructure from arm-specific delivery costs. Treat actual spend and labor separately unless a preregistered conversion is used. Do not extrapolate a per-change saving indefinitely.

## Validity and ethics

Threats: selection, public-code training contamination, task leakage, differential migration budgets, model drift, oracle weakness, order/learning, measurement ambiguity, architecture misclassification, domain/size confounding, instrumentation overhead and survivorship bias. Record mitigation and residual uncertainty per run. Avoid cherry-picking tasks, retries or revisions; document exclusions before execution. Report deviations and preserve failed trials. No real customer data, payments, secrets or paid resources without explicit approval.

## Research grounding

Starting points for literature review (verify versions, citations and relevance before preregistration):
- [ISO/IEC 25010:2023](https://www.iso.org/standard/78176.html) — quality model.
- [SEI Architecture Tradeoff Analysis Method](https://www.sei.cmu.edu/library/the-architecture-tradeoff-analysis-method/) — scenario-oriented evaluation.
- [Modifiability pattern experiment replication repository](https://github.com/xJREB/researchmodifiability-pattern-experiment) — study design and replication comparison.
- [SWE-bench](https://www.swebench.com/) — executable change evaluation; adapt without enforcing implementation details.

Tracking: #2 protocol; #8 pilot analysis; #9 expansion.
