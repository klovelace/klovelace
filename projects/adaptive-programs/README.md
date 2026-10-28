# Adaptive Programs — School Food Impact Lab

**Interactive program monitoring and evaluation demonstration | Glyph Analytics | Simulated data**

[**Launch the live interactive dashboard →**](https://glyphanalytics.com/school-food/)

> **Note:** School Food Impact Lab is a public demonstration built with simulated data. It shows a monitoring and evaluation workflow; it is not a client deployment or a measured impact evaluation.

## The management problem

Program teams frequently have information about **delivery**, **participant experience**, and **outcomes** in separate systems. That makes it difficult to answer the practical question: *What should program managers change next, and what evidence justifies that decision?*

School Food Impact Lab brings those evidence streams together in one interactive monitoring, evaluation, and learning (MEL) experience. Its example domain is school meal implementation and student uptake of plant-based options.

## Evidence-to-action workflow

![Conceptual flow connecting school execution, student experience, impact estimation, and management decisions](assets/evidence-to-action.svg)

### 1. Implementation: did the program happen?

The demonstration supports editable school milestones, implementation blockers, action tracking, and CSV export. Those signals distinguish a theory-of-change failure from a delivery failure: low student uptake means something different if an option was never consistently offered.

### 2. Student experience: why did behavior change—or not?

The dashboard examines familiarity, prior trial, perceived appeal, taste, willingness to repeat, and plate waste. It distinguishes **menu exposure** from **actual selection**, so managers can investigate whether the bottleneck is availability, attractiveness, awareness, or preference.

### 3. Outcomes and counterfactuals: what changed because of the program?

An interactive synthetic-control illustration compares the intervention district with weighted untreated districts. The demonstration includes donor adjustments, untreated trajectories, leave-one-out checks, and placebo tests to communicate how sensitive an estimated effect is to comparator choice. These analyses use **illustrative synthetic data**, not observed district-level causal effects.

### 4. Uncertainty: what should we avoid overclaiming?

The demonstration uses Monte Carlo uncertainty analysis for greenhouse-gas estimates. This is a useful way to present uncertainty in emissions factors, meal substitution, and implementation assumptions rather than publishing a single overprecise environmental-impact number.

### 5. Feedback: what should the team do next?

The theory-of-change evidence panels connect delivery signals, student behavior, outcomes, and operational follow-up. The design supports human decisions about what to investigate or adjust; it does **not** claim that an autonomous AI system is making those decisions.

## What this project demonstrates

| Capability | Public demonstration |
| --- | --- |
| Implementation management | Editable milestones, blockers, actions, and CSV export |
| Theory-of-change monitoring | Linked evidence panels connecting activities to expected outcomes |
| Participant-centered measurement | Familiarity, trial, appeal, taste, repeat selection, and waste |
| Behavioral funnel | Menu exposure versus actual selection |
| Causal-inference communication | Synthetic-control comparison with donor and sensitivity controls |
| Quantifying uncertainty | Monte Carlo greenhouse-gas estimation |
| Management feedback | Evidence organized around operational questions and possible next actions |

## Analytical approach and boundaries

**What is built:** a browser-based interactive dashboard and analytical demonstration with example data and an operational feedback-loop narrative.

**What is illustrated:** monitoring indicators, student preference analysis, synthetic-control diagnostics, and uncertainty visualization. The synthetic-control interface is an explanatory tool, not a verified causal estimate of an actual intervention.

**What is not established:** automated data ingestion from school districts, validated predictive AI models, automated recommendations, field deployment, or measured program impact. “AI for Program Management” describes the broader portfolio theme; this particular artifact primarily demonstrates **decision-oriented analytics and human-in-the-loop evaluation design**.

## Explore

- [Open School Food Impact Lab](https://glyphanalytics.com/school-food/)
- [Visit Glyph Analytics](https://glyphanalytics.com/)
- [Back to portfolio](../../README.md)
