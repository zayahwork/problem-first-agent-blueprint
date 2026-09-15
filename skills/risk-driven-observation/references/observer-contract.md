# Observer contract

Create one record per decision-relevant risk; combine risks only when their signal and response are truly shared.

- **Risk and protected outcome:** Possible loss, affected actor, boundary, and priority source.
- **Signal:** Definition, source, coverage limits, collection frequency, freshness limit, and evidence identity.
- **State model:** Meaning of healthy, degraded, failed, unknown, and stale where applicable; handling for missing or contradictory data.
- **Decision trigger:** Threshold, rationale, and status: existing owner-accepted rule or proposed rule. Name the accepting owner or source when known.
- **Error consequences:** What false alarms and missed detection could cost.
- **Ownership:** Observation owner, decision owner, authorized executor, verifier, and recovery owner as needed.
- **Response:** Recipient, urgency, permitted action, escalation route, review time, and handling if nobody responds.
- **Recovery:** Identified recoverable state, prerequisites, verification, and authority. Mark unavailable or unverified recovery explicitly.
- **Evidence handling:** What is retained, where, for how long, and who may access it, using existing requirements.
- **Cross-effects:** Other outcomes the observation or response could harm, including noise and collection cost.
- **Removal test:** What decision, required evidence, or recovery would become worse without this observer?

When ownership or authority is unknown, mark it unresolved. Do not replace an unanswered question with an invented owner, an automatic rollback, or permission implied by a timeout.
