# OpenSpec Dev Loop Orchestrator Protocol

This file is the persistent working protocol for the Orchestrator agent.

On every user message or heartbeat wakeup, the Orchestrator should read:

1. `.agent-loop/ORCHESTRATOR.md`
2. `.agent-loop/state.md`

The Orchestrator should not rely on conversation memory to advance the workflow. It should rely on these files.

## Core Principles

- The human talks only to the Orchestrator.
- Planner, Executor, and Reviewer are role agents dispatched by the Orchestrator.
- At most one role should modify project files at a time.
- Pause heartbeat whenever human review, manual testing, or confirmation is required.
- Use heartbeat only for "AI waiting on AI" phases, not "AI waiting on human" phases.
- Persist workflow state in `.agent-loop/state.md`.

## Standard Flow

1. Planner writes an OpenSpec change.
2. Human reviews the spec.
3. Executor implements according to the approved spec.
4. Executor commits after each completed implementation pass.
5. Reviewer reviews Executor commits against the spec.
6. If review fails, Reviewer updates spec/tasks and Executor fixes.
7. If review passes, human manually tests.
8. If manual testing fails, Reviewer converts feedback into tasks and Executor fixes.
9. If manual testing passes, Orchestrator archives the change.
10. Orchestrator commits archive/finalization work.
11. Orchestrator pushes if the project workflow requires it.
12. Orchestrator asks whether to start the next change.

## Heartbeat Rules

Heartbeat configuration depends on the current active role.

### Planner

- State phase: `planner_writing_spec` or `planner_reviewing_plan`
- Active role: `planner`
- Waiting for human: `false`
- Heartbeat status: `ACTIVE`
- Suggested RRULE: `FREQ=MINUTELY;INTERVAL=3`
- State interval label: `3 minutes`

### Executor

- State phase: `executor_implementing` or `executor_fixing`
- Active role: `executor`
- Waiting for human: `false`
- Heartbeat status: `ACTIVE`
- Suggested RRULE: `FREQ=MINUTELY;INTERVAL=10`
- State interval label: `10 minutes`

### Reviewer

- State phase: `reviewer_reviewing` or `reviewer_updating_spec`
- Active role: `reviewer`
- Waiting for human: `false`
- Heartbeat status: `ACTIVE`
- Suggested RRULE: `FREQ=MINUTELY;INTERVAL=5`
- State interval label: `5 minutes`

### Human Checkpoint

- State phase: matching `waiting_human_*`
- Active role: `orchestrator`
- Waiting for human: `true`
- Heartbeat status: `PAUSED`
- State interval label: `paused`

## Heartbeat Wakeup Behavior

On heartbeat wakeup:

1. Read `.agent-loop/ORCHESTRATOR.md` and `.agent-loop/state.md`.
2. If phase is `waiting_human_*` or waiting for human is `true`, ensure heartbeat is paused and do not advance.
3. Otherwise inspect only the active role, not every role.
4. If the active role is still running, record a short status update.
5. If the active role has finished:
   - Summarize the result.
   - Update `.agent-loop/state.md`.
   - Dispatch the next role if another AI phase is needed.
   - Pause heartbeat and notify the human if a human checkpoint is reached.

## Human Checkpoints

- Plan review: after initial planning, before detailed spec work if needed.
- Spec review: after Planner completes an OpenSpec change.
- Manual test: after Reviewer approves the implementation.
- Archive confirmation: optional, depending on project release policy.

## Role Dispatch Contract

When dispatching a role, include:

- Current phase
- Current change id
- Relevant spec/task files
- Allowed actions
- Explicit stop condition
- Expected output format

When a role completes, the Orchestrator records:

- Summary
- Files changed
- Commits created, if any
- Tests run
- Blockers
- Next phase
