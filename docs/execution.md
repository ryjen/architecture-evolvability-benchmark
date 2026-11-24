# Execution and reproducibility

No experiment runner, environment or executable tests exist yet. Start with Git, existing project build tools and a minimal structured run record; do not build a new orchestration platform until a demonstrated need.

## Pilot delivery sequence

1. [#2](https://github.com/ryjen/architecture-evolvability-benchmark/issues/2): review/freeze protocol and analysis plan.
2. [#3](https://github.com/ryjen/architecture-evolvability-benchmark/issues/3): qualify candidates; pin medium subject and licenses.
3. [#4](https://github.com/ryjen/architecture-evolvability-benchmark/issues/4): establish S0 and independent oracle.
4. [#5](https://github.com/ryjen/architecture-evolvability-benchmark/issues/5): independently freeze concrete tasks; restrict access.
5. [#6](https://github.com/ryjen/architecture-evolvability-benchmark/issues/6): migrate and qualify arms from S0; record cost.
6. [#7](https://github.com/ryjen/architecture-evolvability-benchmark/issues/7): qualify minimal harness and receipts on non-study task.
7. [#8](https://github.com/ryjen/architecture-evolvability-benchmark/issues/8): execute 36 pilot trials and analyze, including failures.
8. [#9](https://github.com/ryjen/architecture-evolvability-benchmark/issues/9): decide whether to expand to small/large subjects and cumulative evolution.

## Safety and trust

Treat upstream code, build scripts, dependencies, model outputs and patches as untrusted. Use disposable isolated execution environments without host credentials, persistent runner state, private network access or unrestricted egress. Bound time, memory, disk, processes and network; review executable dependencies and pin inputs before execution. Use synthetic datasets and deterministic provider simulators. Do not conduct live financial transactions or connect real customer systems. No paid resources without explicit authorization.

Separate migration implementer, task author, change implementer and independent evaluator roles. Give implementers only task-scoped inputs and tools; the oracle is outside writable scope. Capture exact identities and safe results. A model assertion does not establish a passed test. Store hidden evaluation material separately from public history; publish only approved, sanitized reproduction material after trials are frozen.

## Reproduction requirements

A later replication package should include pinned source and variant identities, dependency/artifact manifests, setup instructions, fixture and oracle versions, frozen task descriptions (when approved for disclosure), execution configurations, randomization seeds, raw sanitized outcomes, analysis scripts and limitations. Preserve license/NOTICE obligations, provenance and negative outcomes. Record every deviation. Human review of claims and redistribution rights precedes publication.

## Unresolved bootstrap decisions

Benchmark implementation language, harness runtime, CI provider, environment format, storage and result distribution remain unresolved until qualification. Candidate Java projects do not imply a Java harness. No deployment, package release or service is required. Existing Apache-2.0 license and main branch are preserved; separate research data/paper licensing is not adopted without explicit approval.
