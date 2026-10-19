# Veiled Vote — Mechanism Design & Institutional AI

**Research prototype | Strategic preference revelation | Multi-agent institutional simulation**

> **Evidence status:** Portfolio research brief. The original simulation repository, executable experiment specifications, and output artifacts have not yet been verified for public release. The hypotheses and experimental comparisons below are a proposed validation framework, **not reported simulation results**.

## 01 · The institutional problem

Collective decisions can fail to reveal what participants actually prefer. When legislators or other agents anticipate retaliation, bargaining costs, or coalition pressure, public statements and recorded votes can diverge from private preferences. Conversely, hiding information can reduce accountability. This project investigates that tradeoff as a **mechanism-design problem**: how do reporting rules change incentives, coordination, and the information available to a collective decision maker?

The purpose is to test institutional designs in controlled simulations, not to claim that a particular voting reform works in real legislatures.

## 02 · Mechanisms under investigation

| Mechanism | Institutional lever | Hypothesized behavior to test |
| --- | --- | --- |
| Public, attributable preference reports | Each participant's stated position is observable | May improve accountability while enabling strategic signaling and pressure |
| Secret preference reports | Individual statements are not publicly attributed | May reduce external pressure but complicate verification |
| Receipt-free reporting | Participants cannot furnish credible proof of their private report to a third party | May limit enforceable side bargains or coercion; requires a credible protocol |
| Independent audits or verification | A separate process checks procedural integrity or aggregate claims | May increase confidence in the process without revealing private reports |
| Structured vignettes | Agents respond to common, specified decision scenarios | May improve comparability, while framing effects remain a concern |

**Important distinction:** Secrecy alone is not receipt-freeness. A mechanism is receipt-free only if a participant cannot reliably prove to another party how they reported. Whether that property holds must be demonstrated by the protocol, not inferred from an anonymous user interface.

## 03 · Simulation design to verify

A defensible experiment would fix a population of agents with heterogeneous policy preferences, party or coalition incentives, reputational concerns, and potential external pressure. It would then vary the reporting mechanism while holding the underlying preference distribution and decision agenda constant.

**Proposed comparison protocol**

1. Define agent utilities, information access, action sets, and whether agents can communicate or coordinate.
2. Specify baseline public reporting and alternative secret or receipt-free mechanisms.
3. Run matched scenarios across mechanisms, with controlled random seeds and multiple agent populations.
4. Record truthful revelation relative to *known simulated latent preferences*, coalition behavior, collective decisions, and attempted manipulation.
5. Stress-test robustness to collusion, misreporting, information leakage, and strategic adaptation.
6. Report uncertainty and failure modes rather than selecting only successful runs.

The original implementation may differ from this proposed protocol. Its details must be reconciled with the source code before any simulation results are published.

## 04 · Evaluation criteria

| Outcome | Operational definition to specify before testing |
| --- | --- |
| Preference revelation | Agreement between a simulated agent's latent preference and its submitted report |
| Decision fidelity | Agreement between the collective decision and a prespecified social-choice objective |
| Strategic misreporting | Rate and consequences of knowingly distorted reports |
| Coalition coordination | Coalition size, stability, and influence under each information regime |
| Coercion and receipt resistance | Whether an adversary can verify, reward, or punish a specific private report |
| Auditability | Ability to verify procedure or aggregates without compromising confidentiality |
| Robustness | Variation across preference distributions, agent strategies, and repeated runs |

These measures can conflict. A design that improves private preference revelation might weaken public accountability, and a mechanism that resists one form of manipulation might enable another.

## 05 · Results and visual evidence

**Results pending source verification.** No quantitative treatment effects, success rates, coalition diagrams, or simulated agent traces are asserted here.

When the original run artifacts are available, the portfolio should show:

- **Mechanism comparison:** outcomes across public, secret, and receipt-free reporting, if actually implemented.
- **Strategic behavior:** original agent traces or aggregate misreporting rates.
- **Coalition structure:** network visualization derived from actual interaction logs.
- **Robustness:** sensitivity to agent preferences, collusion, and adversarial assumptions.

All figures should be produced from the real simulation outputs, with run identifiers, experiment conditions, and limitations.

## 06 · Interpretation and limitations

Agent-based simulations can clarify incentives and expose mechanism failures, but their results depend on behavioral assumptions, agent capabilities, and the modeled institution. Simulated truthful reporting is not direct evidence of human legislative behavior. LLM-driven agents, if used, require additional tests for prompt sensitivity, reproducibility, and model-version effects.

A public technical release would also need a review of repository ownership, confidential material, and publication rights.

### Portfolio status

**Research prototype / public methodology brief.** Mechanisms and evaluation plan documented; implementation, numerical findings, and visual evidence remain unverified. No deployment, real-world legislative validation, or causal effect is claimed.

[Back to flagship portfolio](../../README.md)
