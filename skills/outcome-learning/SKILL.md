---
name: outcome-learning
description: Compare observed results from a probe, release, campaign, or workflow change with its original expectation. Separate operational, adoption, demand, causal, and economic evidence to support bounded learning and the next decision.
---

# Outcome Learning

Turn results into a justified update to a decision. Preserve the original expectation and keep each conclusion within what the evidence can establish.

## Recover the evaluation context

Identify the original problem, hypothesis, expected outcome, exact artifact or workflow version, affected cohort, observation window, baseline or comparison, and decision rule. Locate the source and timing of each. If no prior expectation or threshold exists, say so and label any new one as retrospective and proposed. Do not rewrite history to fit the result.

Verify source identity, freshness, coverage, missingness, sample size, and material measurement changes before comparing outcomes. If evidence is insufficient or invalid for one claim, useful evidence for another claim may still remain.

## Keep conclusions separate

Evaluate only the classes relevant to the question, and label the strength and limits of each:

- **Operational:** Did the system execute correctly, reliably, and within required constraints? A working artifact supports this claim, not customer demand.
- **Adoption:** Did the intended people actually use it, and did relevant use persist? Availability, delivery, and invitations alone do not establish adoption.
- **Demand:** Did intended users show meaningful preference, need, commitment, or willingness to pay in the tested context? Distinguish stated interest from consequential behavior; one transaction does not establish broad demand.
- **Causal:** Did the change produce the observed difference? Examine the comparison design, selection, timing, confounders, and alternative explanations. Correlation or a before-and-after change alone generally leaves causal uncertainty.
- **Economic:** Did the outcome justify total relevant costs and tradeoffs? Include implementation, operation, review, failure, delay, and displaced effort where material. Distinguish measured costs and benefits from estimates. Adoption, revenue, or operational success alone does not prove net value.

Activity counts such as tasks completed, messages sent, or computation consumed may explain operations or cost. They establish higher-level value only when that relationship is supported.

## Update the decision

1. Compare predicted and observed results, including null and negative results, costs, failure modes, and side effects on established priorities.
2. Classify each material claim as supported, contradicted, inconclusive, or invalid for the evidence and window tested. State confidence and the strongest alternative explanation.
3. Identify which belief changed, how far it can generalize, and what remains uncertain. Do not convert a small, selected, or uncontrolled sample into a universal rule.
4. Distinguish an owner-accepted decision threshold from an analyst-proposed threshold. A proposed or retrospective threshold can inform a recommendation but does not become an approved acceptance rule by being written down.
5. Recommend adoption, reversal, holding, or another discriminating probe within the established goals. Name the decision owner, relevant observer, review point, and stop condition. If reversal is suggested, establish what state is recoverable and who can authorize it.

Learning may update a recommendation; it does not silently change policy, strategy, ownership, or execution authority. Carry out a next action only if the user's scope already authorizes it. Keep source evidence within its existing access and reuse boundaries; generalize lessons only where permitted.

For a durable evaluation or handoff, read [references/outcome-record.md](references/outcome-record.md). This skill can interpret evidence directly and does not require a particular analytics tool or another skill.
