---
name: risk-driven-observation
description: Design decision-relevant observation, responsibility, thresholds, and recovery routes for important system or workflow risks. Use when failure, degradation, stale evidence, or unclear response ownership can affect a decision.
---

# Risk Driven Observation

Design the minimum observation needed to detect a meaningful loss and route a useful response. This is an observation design skill; it does not itself install monitoring, create recurring jobs, or grant operational authority.

## Work from risk to response

1. Identify the decision or system boundary, the outcome being protected, and whose outcome it is. Use established priorities; label suggested priorities and their basis.
2. Describe important failures, drift, and loss of visibility. Compare consequence, likelihood or uncertainty, reversibility, and interactions with other protected outcomes. Qualitative comparisons are sufficient when numeric estimates are not grounded.
3. For each risk that could change a decision, choose a signal near the source. State what it measures, what it cannot establish, source identity, sampling or collection limits, and freshness requirements.
4. Define interpretable conditions for healthy, degraded, failed, unknown, and stale where relevant. Missing, contradictory, or old evidence must not silently count as healthy. Do not equate unknown with confirmed failure either.
5. Identify the responsible actor for observation, decision, execution, verification, and recovery when those roles differ. Reuse established ownership and delegation; do not assign new power because an agent can read a signal.
6. Specify the response to a threshold breach or unreliable signal, including recipient, urgency, evidence retained, authorized action, and escalation path. Distinguish a proposed trigger from an owner-accepted operating rule.
7. Check whether the observer or its response creates another material risk, and remove signals that cannot inform a decision, required evidence, or recovery.

Prefer deterministic measurements for known conditions. Use model judgment only where interpretation adds value, with evidence and uncertainty visible to the recipient. Include a way to notice failure of the observation itself when that failure could hide a consequential loss.

## Keep action within authority

A risk signal supports a decision; it does not authorize remediation. Use existing authorization for normal implementation steps when the user requested them. For recovery, identify a known state, feasible procedure, responsible actor, and existing authority. Do not assume the previous state is safe or that restoring it is permitted.

If response authority is unresolved, record the gap and route it to the accountable owner. Pending clarification, stop only the dependent unsafe action and continue useful observation within scope. Propose a bounded review time for unresolved conditions; a deadline does not supply missing authority.

For an operational handoff or formal specification, read [references/observer-contract.md](references/observer-contract.md). This skill is self-contained and can feed a monitoring implementation or review without requiring a specific provider.
