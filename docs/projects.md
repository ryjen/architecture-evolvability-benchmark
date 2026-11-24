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

## Initial source screening (2026-11-24)

This is public-source desk screening, not source qualification. No builds, LOC counts, coupling/cohesion analyses, or immutable revision verification have been completed.

| Candidate | Observed evidence | Qualification implication |
| --- | --- | --- |
| JPetStore | [Official 6.4.0 service API/source](https://mybatis.org/jpetstore-6/xref/org/mybatis/jpetstore/service/OrderService.html) shows constructor-injected mapper interfaces and order/inventory persistence coordination. [Project guide](https://mybatis.org/jpetstore-6/) explains transactional rollback. | Useful for transaction and dependency changes, but third-party breadth and low cohesion are unproven. Do not add artificial coupling. Consider another small candidate if it fails admission. |
| Shopizer | [3.2.7 module configuration](https://github.com/shopizer-ecommerce/shopizer/blob/3.2.7/sm-core/src/main/resources/spring/shopizer-core-modules.xml) defines existing payment and shipping module contracts, provider mappings and mail integration. [Version README](https://github.com/shopizer-ecommerce/shopizer/blob/3.2.7/README.md) describes Java and setup. | Strong integration breadth; existing ports and composition reduce the treatment contrast. Inspect order/pricing workflow dependencies and select only after measuring actual cohesion/coupling. 3.2.7 is a candidate ref, not an immutable SHA. |
| Fineract | [Gradle settings](https://github.com/apache/fineract/blob/develop/settings.gradle) identify accounting and loan-related modules. [Repository](https://github.com/apache/fineract) describes the financial platform. | Strong financial invariants and substantial modularity; define a bounded workflow scope before measurement. Integration count, size and architectural treatment gap remain unknown. |
| Kill Bill | [Project FAQ](https://killbill.io/faqs) describes event-based module coordination; [payment guide](https://docs.killbill.io/latest/userguide_payment) describes provider plugin failure recovery. | Useful alternate or high-modularity comparison. Existing extensibility could make it unsuitable for the intended high-coupling cohort. |

Next: resolve immutable source identities and notices; inspect representative workflows; measure structural properties with a documented tool and sampling rule; qualify a repeatable isolated local build. No candidate is admitted by this screening.

## Shopizer: immutable-source prequalification (2026-11-24)

Source branch 3.2.7 resolved through GitHub to [6a4a0a65a3408ee8f62597b51d1b3aac24b77dee](https://github.com/shopizer-ecommerce/shopizer/commit/6a4a0a65a3408ee8f62597b51d1b3aac24b77dee). All links below use that revision. This is a candidate source pin, not the experimental S0 or admission decision.

### License and build inputs

- [LICENSE.md](https://github.com/shopizer-ecommerce/shopizer/blob/6a4a0a65a3408ee8f62597b51d1b3aac24b77dee/LICENSE.md) and root POM declare Apache-2.0. Root NOTICE, NOTICE.txt and NOTICE.md were not found through the contents API; nested notices, copyright headers, dependency licenses and redistribution obligations remain to be inventoried. Do not redistribute source yet.
- [Root POM](https://github.com/shopizer-ecommerce/shopizer/blob/6a4a0a65a3408ee8f62597b51d1b3aac24b77dee/pom.xml) declares five Maven modules: sm-core-model, sm-core-modules, sm-core, sm-shop-model and sm-shop; compiler target is Java 11.
- [README](https://github.com/shopizer-ecommerce/shopizer/blob/6a4a0a65a3408ee8f62597b51d1b3aac24b77dee/README.md) mentions Java 11/17, while the [Maven wrapper properties](https://github.com/shopizer-ecommerce/shopizer/blob/6a4a0a65a3408ee8f62597b51d1b3aac24b77dee/.mvn/wrapper/maven-wrapper.properties) specify Maven 3.5.2. Compatibility, dependency resolution and build reproducibility require execution; do not infer a working toolchain.
- [Core POM](https://github.com/shopizer-ecommerce/shopizer/blob/6a4a0a65a3408ee8f62597b51d1b3aac24b77dee/sm-core/pom.xml) declares JPA, H2/test dependencies, payment, shipping, search and AWS integrations. Dependency declaration is not evidence of active runtime use.

### Representative workflow evidence

| Source | Direct observation | Interpretation / next check |
| --- | --- | --- |
| [OrderServiceImpl lines 70–105](https://github.com/shopizer-ecommerce/shopizer/blob/6a4a0a65a3408ee8f62597b51d1b3aac24b77dee/sm-core/src/main/java/com/salesmanager/core/business/services/order/OrderServiceImpl.java#L70-L105) | 10 explicit collaborator fields (nine field-injected and one constructor-injected repository); generic persistence superclass | Scoped fan-out proxy, not a measured CBO score. Examine inherited dependencies. |
| [OrderServiceImpl lines 127–213](https://github.com/shopizer-ecommerce/shopizer/blob/6a4a0a65a3408ee8f62597b51d1b3aac24b77dee/sm-core/src/main/java/com/salesmanager/core/business/services/order/OrderServiceImpl.java#L127-L213) | Single workflow coordinates context, payment, status history, customer/order persistence, transactions and inventory. | Natural testability and consistency pressure. Characterize actual behavior with synthetic fixtures before selecting invariants or diagnosing defects. |
| [OrderServiceImpl lines 400–603](https://github.com/shopizer-ecommerce/shopizer/blob/6a4a0a65a3408ee8f62597b51d1b3aac24b77dee/sm-core/src/main/java/com/salesmanager/core/business/services/order/OrderServiceImpl.java#L400-L603) | Same class handles order/cart total calculation, cart updates, deletion, invoice generation, queries and capture-related listing. | Multiple responsibility groups; low cohesion remains a hypothesis until measured. |
| [PaymentServiceImpl lines 53–80](https://github.com/shopizer-ecommerce/shopizer/blob/6a4a0a65a3408ee8f62597b51d1b3aac24b77dee/sm-core/src/main/java/com/salesmanager/core/business/services/payments/PaymentServiceImpl.java#L53-L80) | Seven collaborator fields including OrderService, transaction service and provider map. OrderServiceImpl references PaymentService. | Reciprocal service dependencies in source; verify binding graph and SCCs. Not proof of runtime initialization failure. |
| [PaymentModule](https://github.com/shopizer-ecommerce/shopizer/blob/6a4a0a65a3408ee8f62597b51d1b3aac24b77dee/sm-core-modules/src/main/java/com/salesmanager/core/modules/integration/payment/model/PaymentModule.java) | Existing interface defines configuration validation, initialization, authorization, capture and refund using shared domain/configuration types. | Existing provider abstraction is an important baseline strength; do not count its introduction as a C-arm gain. |
| [Integration composition](https://github.com/shopizer-ecommerce/shopizer/blob/6a4a0a65a3408ee8f62597b51d1b3aac24b77dee/sm-core/src/main/resources/spring/shopizer-core-modules.xml) | Payment/shipping provider maps and mail configuration, including several vendor implementations. | Inventory active versus dormant providers through wiring and isolated execution. |

### Admission disposition

Promising medium candidate with direct workflow evidence of substantial orchestration, responsibility concentration and reciprocal dependencies, despite existing modularity. Still unqualified. Initial source observations are not full structural measurements; no CBO, LCOM4, SCC, propagation-cost, production LOC or runtime regression result exists.

Next required evidence: complete immutable source inventory (including notices), reproducible metric definitions and tool selection, structural measurements at class/module/workflow scope, isolated dependency resolution and build/test receipts, and independently reviewed baseline business contracts. No local execution or real provider access performed.

## Additional immutable candidate pins (2026-11-24)

These are source-inspection snapshots of the current default branches, not accepted releases or S0 baselines. Prefer stable releases if build qualification indicates these snapshots are unsuitable.

| Candidate | Revision | Root license evidence |
| --- | --- | --- |
| JPetStore | [b7433c22c86d634e51646a4fd527fe87694aa6ab](https://github.com/mybatis/jpetstore-6/commit/b7433c22c86d634e51646a4fd527fe87694aa6ab) | [LICENSE](https://github.com/mybatis/jpetstore-6/blob/b7433c22c86d634e51646a4fd527fe87694aa6ab/LICENSE) Apache-2.0; [NOTICE](https://github.com/mybatis/jpetstore-6/blob/b7433c22c86d634e51646a4fd527fe87694aa6ab/NOTICE) present, retain applicable attributions. |
| Fineract | [431eca60184257c97b3427446eed7d152a48cf53](https://github.com/apache/fineract/commit/431eca60184257c97b3427446eed7d152a48cf53) | [settings.gradle](https://github.com/apache/fineract/blob/431eca60184257c97b3427446eed7d152a48cf53/settings.gradle) contains ASF Apache-2.0 header; standard root LICENSE/NOTICE filenames returned 404. Complete license and notice inventory unresolved. |
| Kill Bill | [8881b6617a7ef2d0bd5e1dd354d37405eb1362d6](https://github.com/killbill/killbill/commit/8881b6617a7ef2d0bd5e1dd354d37405eb1362d6) | [LICENSE](https://github.com/killbill/killbill/blob/8881b6617a7ef2d0bd5e1dd354d37405eb1362d6/LICENSE) Apache-2.0; root NOTICE lookup returned 404; remaining inventory unresolved. |

A missing path is not evidence that the tree has no attribution requirements. None of the subjects is cleared for redistribution or formally admitted.
