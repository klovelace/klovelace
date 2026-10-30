# Adaptive Programs — Decision Analytics for Program Management

**School Food Impact Lab | Interactive monitoring and evaluation demonstration | Glyph Analytics | Simulated data**

[**Launch the live interactive dashboard →**](https://glyphanalytics.com/school-food/)

> **Note:** School Food Impact Lab is a public demonstration built with simulated data. It shows a monitoring and evaluation workflow; it is not a client deployment or a measured impact evaluation.

## The management problem

Program teams frequently have information about **delivery**, **participant experience**, and **outcomes** in separate systems, and it reaches them in quarterly or annual reports, after the decisions it could have informed are already made. That makes it difficult to answer the practical question: *What should program managers change next, and what evidence justifies that decision?*

School Food Impact Lab brings those evidence streams together in one interactive monitoring, evaluation, and learning (MEL) system organized around that question. Its example domain is school meal implementation and student uptake of plant-based options.

## The decision loop: Pinpoint → Track → Adjust → Verify

![Pinpoint, Track, Adjust, Verify loop as run in the School Food Impact Lab](assets/evidence-to-action.svg)

Fast feedback on noisy data can teach a team the wrong lesson: they chase random swings and call them progress. The demonstration is built to keep the loop short and the evidence honest.

### 1. Pinpoint: where is the result constrained?

The theory of change follows each stage from district support to district-wide impact, and the dashboard separates **menu exposure** from **actual selection**. That distinction tells a delivery failure apart from a theory-of-change failure: low uptake means something different if the option was never consistently offered.

In the simulated data for all demonstration districts:

| Stage | Indicator | Value |
| --- | --- | --- |
| Program support | Implementation milestones complete | 85% |
| School execution | Meal offered and available at service (opportunity proxy) | **40%** |
| Student experience | Tasters who like the meal | 78% |
| Behavioral change | Share of meals selected | 16.9% |

Students who try the meal mostly like it, and most implementation work is done. The binding constraint is availability at service. More recipe testing or taste campaigns would refine parts that are already within tolerance; reliable availability is where a design change moves the result. This is the same logic engineers use for tolerances: hold tight only the few dimensions performance is most sensitive to.

### 2. Track: what is happening this cycle?

School-level milestones, availability, meal selections, and student feedback update monthly. Student measures cover familiarity, prior trial, perceived appeal, experienced taste, willingness to repeat, and plate waste, so a drop in selection can be traced to a cause rather than reported as a number.

### 3. Adjust: who acts on it?

Implementation blockers become corrective actions with an owner and a deadline, tracked in an editable action queue with CSV export. Theory-of-change evidence panels link each signal to the management response it should trigger. The design supports human decisions about what to investigate or change; it does **not** claim that an autonomous AI system is making those decisions.

### 4. Verify: did it work, and how sure are we?

An interactive synthetic-control illustration compares the intervention district with weighted untreated districts, with donor adjustments, untreated trajectories, leave-one-out checks, and placebo tests that show how sensitive an estimated effect is to the choice of comparison. Greenhouse-gas estimates use Monte Carlo uncertainty analysis across emissions factors, meal substitution, and implementation assumptions rather than a single overprecise number. These analyses use **illustrative synthetic data**, not observed district-level causal effects.

## What this demonstrates for decision science leadership

- **Decision-first design.** Every view answers an operational question a manager has to act on, not a reporting requirement.
- **Finding the constraint before optimizing.** Separating exposure from selection prevents a team from spending a cycle fixing taste when the problem is supply.
- **Distinct kinds of evidence.** Delivery records, stated opinions, observed behavior, and modeled impact are kept separate, each with its own denominator and caveats.
- **Honest uncertainty.** Counterfactual sensitivity and modeled uncertainty bands are shown, not hidden behind a single estimate.
- **Accountable ownership.** Evidence ends in a named owner and a next action, then gets re-checked the following cycle.

| Capability | Public demonstration |
| --- | --- |
| Constraint diagnosis | Theory-of-change stages and menu exposure versus actual selection |
| Implementation management | Editable milestones, blockers, owner-assigned actions, and CSV export |
| Participant-centered measurement | Familiarity, trial, appeal, taste, repeat selection, and waste |
| Causal-inference communication | Synthetic-control comparison with donor and sensitivity controls |
| Quantifying uncertainty | Monte Carlo greenhouse-gas estimation |
| Management feedback | Evidence organized around operational questions and next actions |

## Analytical approach and boundaries

**What is built:** a browser-based interactive dashboard and analytical demonstration with example data and an operational feedback loop.

**What is illustrated:** monitoring indicators, constraint diagnosis, student preference analysis, synthetic-control diagnostics, and uncertainty visualization. The synthetic-control interface is an explanatory tool, not a verified causal estimate of an actual intervention.

**What is not established:** automated data ingestion from school districts, validated predictive AI models, automated recommendations, field deployment, or measured program impact. This artifact demonstrates **decision-oriented analytics and human-in-the-loop evaluation design**.

## Explore

- [Open School Food Impact Lab](https://glyphanalytics.com/school-food/)
- [Visit Glyph Analytics](https://glyphanalytics.com/)
- [Back to portfolio](../../README.md)
