# Problem First Agent Blueprint

A portable starting point for projects that use AI agents to investigate problems, deliver bounded work, recover from interruptions, and learn from results.

The central idea is simple: preserve why the work matters, what is known, who owns the next action, and the evidence that justifies continuing.

**Status: saved architecture blueprint and reusable instructions.** This repository contains documentation, four agent skills, templates, and a fictional example. It does not contain a running orchestrator, provision infrastructure, connect accounts, or demonstrate production reliability or measured token savings.

## Start here

1. Read the [operating model](docs/operating-model.md).
2. Fill in one [work packet](templates/work-packet.md) for a small internal problem.
3. Use the relevant [skill](#reusable-skills) to investigate, build evidence, or resolve a conflict.
4. Follow the [coordination and recovery contract](docs/coordination-and-recovery.md) when implementing automation.
5. Apply the [context and evaluation plan](docs/context-and-evaluation.md) before claiming improvements.

For a complete walkthrough, see the [fictional lead handoff pilot](examples/lead-handoff-pilot.md).

## The operating idea

Problem and governing priorities → evidence → proposal → bounded action → verification → outcome review

New evidence can reopen earlier decisions. This is a reasoning path, not a requirement to create seven tickets or agents for every change. Routine work can inherit an accepted problem and decision.

The system maintains three separate facts:

| Fact | Example |
| --- | --- |
| Work item | A reviewer accepted the requested implementation. |
| Execution attempt | A particular worker finished, yielded, failed, or has an unknown disposition. |
| External effect | A provider confirmed an action, rejected it, or has not established what happened. |

A completed build can have a linked business experiment that is still measuring results. An unanswered request to a provider remains unknown until reconciled.

## Suggested tool responsibilities

| Responsibility | Possible implementation |
| --- | --- |
| Visible work, owners, dependencies, decisions | Linear or another issue tracker |
| Versioned knowledge, instructions, code, workflow definitions | GitHub or another version control host |
| Dispatch, events, scheduled resumptions | n8n or another workflow runner |
| Durable attempts, checkpoints, action intents, accepted transitions | A database or existing execution ledger |
| Bounded investigation, implementation, review, measurement | Available agent tools and workers |
| Business priorities and consequential tradeoffs | The accountable human owner |

These are responsibilities to implement. Using these products alone does not create the coordination protocol. The blueprint works without committing to a particular model, subscription, machine, or vendor.

## Reusable skills

Each directory is self-contained. Read its `SKILL.md` when relevant and load its reference only when preparing a durable record.

| Skill | Use it when |
| --- | --- |
| [Problem first framing](skills/problem-first-framing/SKILL.md) | The cause or intended outcome needs investigation. |
| [Risk driven observation](skills/risk-driven-observation/SKILL.md) | You need to know what could fail and how to notice it. |
| [Quorum and cycle control](skills/quorum-cycle-control/SKILL.md) | Specialists conflict or repeatedly reverse shared decisions. |
| [Outcome learning](skills/outcome-learning/SKILL.md) | Evidence is available to compare with the original expectation. |

To use a skill with a compatible agent tool, install the selected directory in that tool's skill location according to its instructions. With another tool, provide the relevant Markdown as task guidance. No automatic installer or connection is included.

## Long projects and context efficiency

A project can continue through many bounded sessions when durable state and resumption are implemented. A fresh worker receives the relevant problem slice, exact artifacts, current decisions, permitted actions, checkpoint, and next step.

Potential savings come from selective retrieval, reusable verified results, shorter handoffs, and fewer repeated mistakes. Review and coordination also cost resources. Measure total effort per accepted result, including retries and reviewers; the repository makes no percentage or quality guarantee.

Skills and stored knowledge guide behavior. They do not retrain model weights or make every connected agent adopt the protocol automatically.

## Implement in stages

1. Establish one authoritative home for each kind of record.
2. Prove one internal task from assignment through evidence and review.
3. Exercise interruption, duplicate delivery, stale output, and checkpoint recovery.
4. Test external effects with a fake provider before enabling real actions.
5. Add cycle detection and a bounded conflict decision.
6. Measure a real pilot and expand where evidence justifies it.

An implementation is ready for unattended operation only when its claimed behaviors have passed the relevant tests. See [adoption gates](docs/context-and-evaluation.md#adoption-gates).

## Source and attribution

The design was inspired by user-supplied material attributed to Nes / `@nestharus` and refined into this generic synthesis. [Source notes](docs/source-notes.md) distinguish those ideas from the implementation choices in this repository. Source books and private operational records are not distributed here.
