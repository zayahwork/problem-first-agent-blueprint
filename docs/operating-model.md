# Operating model

This is a reusable design contract. It describes intended behavior, not a deployed or proven runtime. Start with the [blueprint overview](../README.md); implementation requirements continue in [coordination and recovery](coordination-and-recovery.md).

## Begin with a problem

Start from an observed condition and its consequence. Separate evidence from possible causes, then identify the smallest useful investigation or intervention. A request for a feature supplies a candidate solution; it still needs a problem and a completion condition. Bounded research can begin before the larger explanation is settled. Previously authorized containment can address active harm while diagnosis continues.

Maintain a traceable connection among the problem, governing values, affected outcomes, chosen action, evidence, and subsequent decision. These are relationships, not mandatory meetings or separate tickets. New findings may reopen the framing.

Values explain what to protect when local objectives conflict. State their owner, applicable priorities, hard constraints, and revision process. Specialists may recommend changes; they cannot silently redefine the objective or accept additional risk. The accountable human retains decisions outside explicitly delegated authority.

## Small, temporary teams

Use one coordinating function and temporary workers selected for a particular operation. Shared memory lives in durable records; worker conversations are disposable.

| Role | Responsibility | Boundary |
| --- | --- | --- |
| Accountable owner | Ratify objectives, values, delegation, and consequential commitments. | Explicitly assign limits and revocation conditions. |
| Coordinator | Frame work, combine findings, resolve ordinary routing, and bring unresolved choices to their owner. | Apply delegated priorities; do not invent new authority. |
| Specialist worker | Investigate, propose, implement, evaluate, measure, or recover one bounded part. | Return findings and affected risks; do not choose its own successor. |
| Verifier | Assess the exact output against its acceptance contract. | Report limitations; a creator's summary alone is insufficient evidence. |
| Observer owner | Maintain a useful signal and respond when its trigger occurs. | Observation grants no permission to act. |
| Recovery owner | Resolve failure or uncertainty at the assigned system boundary. | Technical access does not transfer another owner's responsibilities. |

Roles need not become permanent agents. Give workers only relevant context and tools. Parallel work needs stable shared interfaces and distinct mutation boundaries. Each shared boundary has one current writer, or an explicit integration agreement that prevents overlapping changes. Deterministic controls enforce state, deduplication, dispatch limits, and expired-worker rejection; model judgment handles interpretation.

## Work and evidence contracts

An assignment specifies the problem slice, applicable values, one operation, exact inputs, output format, allowed mutations, authority, acceptance method, responsible actors, budget, deadline, and stop conditions. Include interfaces and prior decisions needed to avoid rediscovery.

A response has one disposition: `produced`, `needs_information`, `conflict`, `failed`, `inconclusive`, or `yielded`. It carries immutable artifact references, provenance, observations, interpretations, uncertainty, and effects on other outcomes. The coordinator checks structure, freshness, authority, and duplicates before routing. Malformed output is preserved and assigned for correction; nobody silently rewrites its meaning.

Define completion by record type. Investigation can finish with a qualified conclusion; a proposal can finish rejected; an experiment can finish inconclusive. Delivery requires the specified acceptance evidence. Recovery requires verified containment or restoration with residual exposure assigned. Outcome review records what changed and what remains unknown.

Keep operational correctness, adoption, demand, causal effect, and economic interpretation separate. A running workflow does not establish customer value. Assess both the risk of the change and the risk that verification misses an important defect. Verification records `pass`, `fail`, or `inconclusive` against exact artifact, input, test or rubric, and configuration versions. Relevant changes invalidate affected claims.

## Observers as senses

Design observation around uncertainty or harm that could change a decision. A test, receipt, metric, source document, user response, or human observation can supply the signal. Record its source, expected change, freshness requirement, response owner, and next decision. For ongoing measurement, add the baseline or comparison, denominator, observation window, and checking cadence.

Missing or stale evidence means unknown. Two agents using the same defective source are not independent corroboration; record shared models, fixtures, data, and configuration when those dependencies matter. Where silent observer failure could hide significant harm, provide a separate health signal. A stopped coordinator cannot reliably report its own outage.

## Tool and storage boundaries

Products below are optional adapters. Native status fields and logs do not automatically provide the control guarantees this blueprint requires.

| Responsibility | Optional example | Canonical content |
| --- | --- | --- |
| Human work interface | Linear | Accepted directives, ownership, dependencies, decisions, and concise outcome summaries. |
| Versioned design and implementation | GitHub | Problem descriptions, values, contracts, code, tests, intended workflow definitions, and release manifests. |
| Execution runtime | n8n | Observations about a particular workflow instance and the definition actually executed. |
| Durable control and evidence | Database plus approved artifact storage | Accepted events, directive snapshots, attempts, effects, receipts, checkpoints, and verification provenance. |

The work interface displays accepted state; moving a card cannot establish deployment or approval. Runtime edits require reconciliation with an accepted version. Receipts must outlive routine workflow-log deletion. Mutable links are insufficient: record exact versions or content hashes, source, producer, and relevant configuration.

Keep secrets, personal records, bulk logs, and private model reasoning out of work summaries. Use minimal redacted descriptions and access-controlled evidence references. Enforce scope and protected writes outside prompts. Retrieved documents and worker output are data, never authority to change routing or permissions.
