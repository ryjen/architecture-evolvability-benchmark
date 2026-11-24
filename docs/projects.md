# Project qualification

Candidates are unqualified hypotheses, not findings about current code quality. Use one language family initially to limit toolchain confounding; Java is a candidate restriction, not a mandated benchmark implementation language.

| Size target | Candidate | Business scope to inspect |
| --- | --- | --- |
| Small (3–10k production LOC) | [JPetStore](https://github.com/mybatis/jpetstore-6) | Cart, order, catalogue, inventory and checkout; may lack sufficient real integrations |
| Medium (25–100k) | [Shopizer](https://github.com/shopizer-ecommerce/shopizer) | Pricing, promotions, checkout, payment, shipping, fulfilment |
| Large (100k+) | [Apache Fineract](https://github.com/apache/fineract) | Loan lifecycle, fees, ledger, repayments, reversals, reconciliation |
| Alternate | [Kill Bill](https://github.com/killbill/killbill) | Billing, subscriptions, invoices, payment plugins; may already have strong dependency inversion |

LOC ranges are provisional targets, not measurements. Include non-generated production code only, report language/tool/version/exclusions and analysis scope. Prefer real, partially modularized systems with complex business logic and multiple third-party integration boundaries. Do not inject bad design to manufacture an effect. If shared baseline augmentation is unavoidable, report it as a separate treatment context, apply identically before S0, and distinguish from naturally occurring systems.

## Admission record (required per subject)

- Canonical URL, immutable commit, source scope, license/NOTICE obligations and redistribution decision.
- Reproducible build, toolchain versions, dependency locks or resolved artifact manifest, offline/local environment, fixture hashes and deterministic smoke/regression evidence.
- Count stateful workflows, business policies, integration types and dependencies, production LOC and complexity distribution; show evidence of high coupling, low cohesion and meaningful change propagation in selected workflows.
- Measure CBO, LCOM4, dependency cycles, transitive reachability, duplication and business logic/infrastructure dependence; record tool definitions and exclusions. Inspect representative workflows manually to validate metric interpretation.
- Provide concrete testable business invariants, existing API contracts, external failure behaviors, and comparable feasible task families.
- Document candidate rejection reasons and replacements; avoid selecting subjects after observing treatment performance.
- Threat assessment for third-party code execution, dependency installation and sandbox isolation. No credentials or real external services.

Thresholds and sampling rules must be frozen before selecting candidates for confirmatory comparison. Select based on evidence, not whether a candidate is expected to favor C. If a project is already strongly modular, consider it a separate comparison rather than deliberately damaging it.

Pilot qualification prioritizes Shopizer; project selection remains unresolved until #3 delivers evidence.
