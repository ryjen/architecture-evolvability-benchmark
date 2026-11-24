# Architectural Evolvability Benchmark (AEB)

An empirical benchmark investigating whether Clean Architecture and SOLID reduce the cost of delivering correct business changes, relative to existing architecture and conventional modular refinement.

**Status: experimental; protocol proposed, no qualified subjects or measured results yet.** Not production software or evidence that any architecture is superior.

## Research design

Compare independent variants derived from the same source revision:

- A: existing architecture, with ordinary task-local refactoring permitted.
- B: conventional modular refinement, with no prescribed architectural style.
- C: Clean Architecture and SOLID, with inward dependency direction and justified boundaries.

Measure accepted business outcomes, regression risk, testability, engineering effort and cumulative cost, including the initial architecture investment. Report null and adverse results.

Start with a medium-project pilot: four task families, three arms, three repetitions (36 independent trials). Small and large subjects follow only after pilot qualification.

## Documentation

- [Research protocol](docs/protocol.md) — hypotheses, controls, arms, analysis.
- [Project qualification](docs/projects.md) — candidate sources and admission criteria.
- [Measurement contract](docs/measurements.md) — outcomes, accounting and evidence.
- [Business scenario catalogue](docs/scenarios.md) — task families and oracle design.
- [Execution and reproducibility](docs/execution.md) — isolation, sequencing and pilot gates.

## Getting involved

See [pilot epic #1](https://github.com/ryjen/architecture-evolvability-benchmark/issues/1) and [open issues](https://github.com/ryjen/architecture-evolvability-benchmark/issues). Review the protocol before proposing implementation. No build or reproduction command exists yet; candidate and harness work is tracked in issues #3–#7.

Use synthetic data and simulated providers. Never submit credentials, customer data, hidden evaluation inputs or sensitive diagnostics in public issues. Report security concerns privately to the repository owner.

## License

Original repository material is covered by [Apache-2.0](LICENSE). Third-party source remains subject to upstream terms and notices; no upstream source is included at this stage. Any distinct future dataset or paper license requires an explicit decision before distribution.
