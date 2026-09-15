# Coordination and recovery

These are proposed control contracts, not implemented guarantees. See the [operating model](operating-model.md) and [blueprint overview](../README.md). An implementation must prove the transitions and failure behavior below before claiming unattended reliability.

## Three distinct state machines

Work acceptance, worker execution, and external effects answer different questions. Every transition needs an authenticated owner, current directive, evidence, and an accepted event. Reject unlisted transitions. Replayed events return their existing receipt without repeating work or effects.

### Work item

Capture creates `Triage`. An active state is any state except `Done` or `Canceled`.

| From | Event → next state | Guard |
| --- | --- | --- |
| Triage | Prepared → Ready | Bounded operation, inputs, owners, authority, acceptance, and stop condition exist. |
| Ready | Start acknowledged → In Progress | Current attempt, lease, and input versions match. |
| In Progress | Output submitted → In Review | Durable valid output exists; effects are settled or quarantined with dependent claims blocked. |
| In Review | Accepted → Done | Required verifier checks the exact completion condition. |
| In Review | Correction authorized → Ready | Preserve failed evidence; bound a new attempt within current authority. |
| Any active | Blocker recorded → Waiting | Record reason, owner, previous state, resume condition, next action, and relevant deadline. |
| Waiting | Resume authorized → Ready | Blocker cleared; inputs, purpose, and authority remain current. |
| Waiting | Review unblocked → In Review | Existing output is reviewable without repeating execution. |
| Waiting | Reframing authorized → Triage | Preserve the old directive; reopening grants no execution authority. |
| Any active | Cancellation settled → Canceled | Disable dispatch; settle in-flight effects or transfer exposure to an owned incident. |
| Done / Canceled | Reopening authorized → Triage | Material changes justify a new directive revision. |

A cancellation request immediately blocks new dispatch and puts unsettled work in `Waiting`. Waiting reasons distinguish decisions, dependencies, measurement, validation, reframing, runtime uncertainty, recovery, invalid output, and cancellation. Reason changes preserve the last non-waiting state and history. A rollback has its own receipt and explicit disposition; it does not prove the cause is fixed.

### Execution attempt

Queueing creates `Queued` only for a current ready directive with a dispatch reservation. A queue entry grants no mutation rights.

| From | Event → next state | Guard |
| --- | --- | --- |
| Queued | Worker started → Running | Current lease and directive acknowledged. |
| Queued | Dispatch rejected → Failed | Evidence proves the worker never started. |
| Queued | Dispatch unacknowledged → Unknown | Worker may have started. |
| Queued | Canceled before dispatch → Canceled | Evidence proves dispatch never occurred. |
| Running | Checkpoint accepted → Yielded | Durable continuation record; mutation rights released. |
| Running | Output recorded → Succeeded | Contracted output and provenance are durable; acceptance remains separate. |
| Running | Failure established → Failed | Preserve evidence and assign unresolved effects. |
| Running | Stop confirmed → Canceled | Stop and mutation-boundary disposition are known. |
| Running | Lease or acknowledgment lost → Unknown | Revoke mutation rights and reconcile. |
| Unknown | Outcome reconciled → Succeeded / Failed / Canceled | Independent runtime or artifact evidence establishes the result. |
| Unknown | Checkpoint recovered → Yielded | Validate checkpoint and fence off the old worker. |

`Yielded`, `Succeeded`, `Failed`, and `Canceled` end that attempt. Continuation creates a new attempt linked to its predecessor. A safe read-only investigation may proceed while an older attempt remains unknown; it cannot repeat uncertain effects or admit late writes.

### Consequential effect

A durable intent creates `Prepared`. Record the exact action, destination, scope, authority, limits, expiry, workflow version, confirmation predicate, logical effect key, and recovery owner.

| From | Event → next state | Guard |
| --- | --- | --- |
| Prepared | Dispatch committed → Dispatched | Final authority, eligibility, version, stop-state, executor, and budget checks pass. |
| Prepared | Preflight rejected → Rejected | Evidence proves no dispatch occurred. |
| Dispatched | Effect confirmed → Confirmed | Provider or source evidence satisfies the declared confirmation predicate. |
| Dispatched | No effect confirmed → Rejected | Evidence proves the action did not take effect. |
| Dispatched | Outcome uncertain → Unknown | Timeout, crash, or ambiguous acknowledgment leaves uncertainty. |
| Unknown | Reconciled → Confirmed / Rejected | Provider lookup or assigned investigation establishes the outcome. |

Persist intent and reserve shared allowances atomically before the provider call. A stop ordered before dispatch commitment prevents dispatch; a later stop requires reconciliation and cannot promise retraction. A crash around dispatch remains uncertain; retain its reservation. One logical action keeps one stable effect key. Retransmit only with verified, operation-specific provider idempotency; otherwise investigate before retrying. Replacement after proven rejection and compensation require separate linked, authorized intents. Acceptance, delivery, response, and business effect are distinct claims.

## Durable reconciliation

Persist directive revisions and controlling-content hashes, attempt leases, effect intents, events, checkpoints, decisions, and immutable evidence references. Use an inbox for incoming events and a transactional outbox for dispatch and display updates. Accept a transition only if its expected state and revision still match. Deduplicate event keys. Increasing lease tokens must be enforced at every protected write boundary so expired workers cannot bypass revocation.

Treat work-interface edits as commands requiring validation. Runtime observations supply evidence, not unquestionable truth. Preserve disagreements; quarantine stale or out-of-order results until their prerequisites can be reconciled. A useful late artifact may be retained without advancing current work.

Project accepted transitions back to the work interface with an origin and revision to prevent feedback loops. Retry failed projections without claiming unverified completion. Reconcile concurrent human edits instead of overwriting them. Lost connectivity cannot authorize new commitments. On restart, inspect leases, unknown effects, pending events, outbox messages, and checkpoint integrity before dependent dispatch.

A checkpoint gives a fresh worker the current problem, exact artifacts, completed work, decisions and rationale, relevant values, unresolved questions, failed approaches, effect dispositions, blockers, and first safe next action. Store decision rationale, not private reasoning. Define retention and restore procedures, independent coordinator health checks, and deadlines for recovery ownership. Heartbeats show activity; accepted artifacts, resolved uncertainty, and verified results show progress.

## Repetition and conflict

For each decision question and affected boundary, retain a versioned context fingerprint, meaningful before/after state fingerprints, new evidence, superseded rulings, and recovery references. Include governing problem and value versions, material inputs, relevant environment, and the evidence frontier.

Normalization excludes incidental timestamps, wording changes, token counts, and unrelated comments. Include windows, cohorts, seeds, and freshness when they affect meaning. Exact hashes establish equivalence only within that contract; semantic resemblance requires review.

| Condition | Detection and disposition |
| --- | --- |
| Duplicate | Equivalent reusable operation and fresh inputs already verified: reuse evidence with a receipt, never infer reusable authority or permission to repeat an effect. |
| Oscillation | Meaningful state returns A → B → A under unchanged governing evidence: pause that boundary and examine the conflict. |
| Rediscovery | Same question returns without invalidation evidence: retrieve the earlier ruling. |
| Deadlock | Closed dependencies have no independently satisfiable input: record the cycle and assign a bounded break or reframing decision. |
| Stall | Declared progress window expires without progress or legitimate wait: request a checkpoint or reconcile, then escalate to the recovery owner. |

Authorized rollback, new evidence, revised values, and a new experimental cohort can justify revisiting a state. A scheduled measurement wait is legitimate until its condition expires. Additional review findings can represent learning. Repeat counts are alerts, not proof of failure or convergence. Preserve compared fingerprints and changes; freeze only affected branches unless the risk is global.

## Quorum without voting

Use a bounded conflict review when existing priorities do not resolve materially opposed recommendations, or changes repeatedly reverse. Freeze the question, candidate and input versions, required affected-outcome owners, synthesis owner, independent evidence verifier, authorized decider, evidence standard, exchange limit, deadline, and cost budget. Pause shared mutations during review; separately authorized urgent containment may proceed.

Participants submit durable positions against the same evidence: intended benefit, harm elsewhere, uncertainty, objections, and evidence that would change their view. Exchange responses to specific objections. Verification reports `pass`, `fail`, or `inconclusive` within its stated boundary. The coordinator synthesizes; the authorized owner rules. Agreement from models sharing a source does not create independent evidence.

Sufficiency requires required perspectives, adequate verification, disposition of material objections, and authority for the ruling. Only the accountable human may authorize participant substitution or accept a missing perspective. Silence and majority preference create no approval. Hard boundaries cannot be averaged away.

Record `decided`, `needs_evidence`, `needs_human_decision`, or `stopped`; a decision marks each candidate selected, rejected, or deferred. Preserve dissent, accepted local losses, exact versions, execution owner, review point, and reversal evidence. Expired limits end debate with an owned investigation, a precise unresolved choice, or a stop. Timeout never authorizes action. Material changes require a new decision revision and refreshed affected positions. Recurring unchanged conflict or disputed authority escalates to the accountable human. External dispatch still requires its own current effect checks.
