# Context, evaluation, and adoption

## A small context packet

The complete project history lives in durable storage. A worker receives only the material relevant to its assigned operation, with links back to the full evidence.

Include:

1. Work ID, directive revision, operation, and responsible owner.
2. The accepted problem slice, desired result, and relevant governing priorities.
3. Exact input versions and evidence references, with uncertainty preserved.
4. Allowed actions, applicable constraints, and the expected output.
5. Relevant prior decisions, unresolved objections, and invalidation conditions.
6. The current checkpoint, affected external actions, stop condition, and next step.

Metadata such as attempt IDs, leases, and timestamps should be supplied by the integration when it exists. Do not ask a human to reconstruct runtime state from memory.

## Retrieve progressively

Start with a title index and short descriptions. Open the relevant document, then the relevant section, then its original evidence if the decision requires it. Provide a path to recover the complete record.

Keep hard constraints, unresolved objections, evidence limitations, and action boundaries in view. Compress repeated background more aggressively than decision-critical information. If omitted material could change the action, retrieve it before proceeding.

A saved decision can be reused only while its inputs, governing priorities, authority, and freshness remain applicable. A cached completion cannot authorize another external effect.

A skill is instruction. Memory is retained information. A checkpoint is resumption state. None of these alone changes model weights.

## Honest measurement

Compare the existing workflow with the proposed workflow on the same task distribution and declared acceptance conditions. Keep an evaluation set separate from development examples. Where feasible, alternate order or use matched trials to reduce environmental bias.

| Measure | Include |
| --- | --- |
| Accepted result quality | Task-specific behavior, critical omissions, problem coverage, and downstream side effects |
| Context load | Initial input plus later retrieval, repeated history, and cached input reported separately |
| Total model usage | Coordinator, workers, reviewers, retries, and failed attempts |
| End-to-end duration | Queue delay, human waiting, execution, review, and recovery |
| Human effort | Clarification, corrections, approvals, and manual recovery |
| Reliability | Duplicate effects, stale results, unresolved states, and successful interruption recovery |
| Business outcome | Adoption, useful customer progression, costs, and eventual value with observation limits |

Report source, observation window, exact versions, and sample counts. Use provider-reported usage when available; otherwise label estimates. Do not infer exact dollar cost or remaining subscription allowance from token counts without a valid mapping. Local workflow steps use compute, and model calls through a CLI can still consume subscription allowance.

Savings are measured against a defined baseline, not predicted from the number of skills. Review or debate may increase usage while reducing expensive errors. Compare total effort per accepted result and preserve failed or inconclusive trials.

## Behavioral scenarios

Skill metadata and links can be checked structurally. These scenarios test the decisions the instructions produce; an implementer must actually run and record them before claiming a pass.

| Scenario | Expected behavior |
| --- | --- |
| A customer asks for a CRM without evidence about missing leads | Preserve the request, investigate plausible causes, and select a bounded probe. |
| Two agents alternate a policy under unchanged evidence | Detect the repeated meaningful state, pause affected changes, and resolve the conflict. |
| A rollback returns to an earlier version after a real incident | Treat authorized recovery as distinct from dysfunctional oscillation. |
| A reviewer repeats the creator's summary | Identify the shared evidence limitation and inspect the underlying work. |
| Three agents favor a change that violates a hard boundary | Preserve the boundary; voting cannot authorize the change. |
| A small test produces more activity and no measured profit | Separate activity, adoption, effect, and economic claims; preserve uncertainty. |
| A prompt demands a universal 10% cohort or fixed debate length | Treat numbers as proposals needing a reason and an accountable owner. |

## Adoption gates

Use only the gates relevant to the capability being enabled. A repository of instructions can be useful before it runs autonomously.

### 1. Internal task

Assign one reversible operation, store its result, independently inspect the declared behavior, and project the accepted state to the issue tracker. A queued task must not appear as an acknowledged running task.

### 2. Interruption and replay

Lose an acknowledgment, deliver a duplicate event, submit a stale result, restart a worker, and resume from a checkpoint. Require preserved history and one accepted mutation. A heartbeat must not count as substantive progress.

### 3. External action simulation

Use a fake provider. Test a crash before dispatch, a timeout after the provider accepted the action, revoked authorization, changed recipient or scope, and replay. Preserve unknown outcomes until reconciled. Recheck authority and limits immediately before dispatch.

### 4. Conflict and liveness

Exercise one real conflict, a missing specialist, an expired debate budget, a dependency deadlock, a valid measurement wait, and a stopped coordinator. Require an owned next action and a response proportional to the affected boundary.

### 5. Pilot value

Record operational correctness, user adoption, demand, causal evidence, economic plausibility, and costs separately. A negative finding can finish an experiment successfully as research while rejecting the proposed intervention.

For each gate, retain the tested version, scenario, evidence source, expected versus actual behavior, disposition, and remaining uncertainty. A pass expires when relevant assumptions or artifacts change.
