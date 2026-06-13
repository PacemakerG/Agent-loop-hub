# OpenSpec Dev Loop

A Planner-Executor-Reviewer loop for semi-automated software development with human checkpoints.

This loop is designed for software projects that use OpenSpec-style changes and want AI agents to collaborate in a repeatable, resumable way.

## Core Idea

The human talks to one Orchestrator agent.

The Orchestrator coordinates three role agents:

- Planner: turns intent into a plan and OpenSpec change.
- Executor: implements the approved spec and commits code.
- Reviewer: reviews implementation against the spec and sends fixes back.

State is stored in the project, usually under `.agent-loop/state.md`, so the workflow can continue after context loss, failures, or long pauses.

## Flow

```text
Plan -> Spec -> Implement -> Review -> Human Test -> Fix -> Archive
```

Expanded:

```text
Planner writes plan/spec
  ->
Human reviews spec
  ->
Executor implements and commits
  ->
Reviewer reviews implementation
  ->
If review fails:
  Reviewer updates spec/tasks
  Executor fixes and commits
  Reviewer reviews again
  ->
If review passes:
  Human tests manually
  ->
If human test fails:
  Reviewer updates spec/tasks from feedback
  Executor fixes and commits
  Reviewer reviews again
  ->
If human test passes:
  Orchestrator archives the change
```

## Roles

### Orchestrator

The Orchestrator is the only agent that talks directly with the human.

Responsibilities:

- Read `ORCHESTRATOR.md`.
- Read `.agent-loop/state.md`.
- Dispatch Planner, Executor, and Reviewer.
- Update state after each phase.
- Manage heartbeat polling.
- Pause at human checkpoints.
- Summarize progress and next actions.

### Planner

The Planner owns planning and spec writing.

Responsibilities:

- Write the overall implementation plan.
- Create OpenSpec proposal/design/tasks/spec deltas.
- Avoid business-code implementation.
- Stop after planning and wait for human approval through the Orchestrator.

### Executor

The Executor owns implementation.

Responsibilities:

- Implement only the approved spec/tasks.
- Avoid changing the plan or spec unless instructed.
- Run relevant tests.
- Commit each completed implementation or fix.
- Report commit hashes and verification results.

### Reviewer

The Reviewer owns review and feedback capture.

Responsibilities:

- Review Executor commits against the approved spec.
- Identify blocking issues, behavior drift, test gaps, and regression risks.
- When review fails, update spec/tasks with required fixes.
- When human testing fails, turn feedback into concrete tasks.
- Avoid implementing code unless the Orchestrator explicitly authorizes it.

## Recommended Project Files

Add this directory to the target project:

```text
.agent-loop/
  ORCHESTRATOR.md
  state.md
```

Use the templates in this loop:

- `ORCHESTRATOR.md`
- `state.template.md`
- `planner.prompt.md`
- `executor.prompt.md`
- `reviewer.prompt.md`

## Heartbeat

Heartbeat polling is useful when one agent is waiting for another agent.

It should not run while waiting for the human.

Suggested intervals:

- Planner phase: every 3 minutes
- Executor phase: every 10 minutes
- Reviewer phase: every 5 minutes
- Human checkpoint: paused

Recommended phases:

```text
planner_reviewing_plan
planner_writing_spec
waiting_human_plan_review
waiting_human_spec_review
executor_implementing
implementation_committed
reviewer_reviewing
reviewer_updating_spec
waiting_human_manual_test
executor_fixing
archiving_change
archive_committed
pushing_change
ready_for_next_change
```

## Human Checkpoints

Pause and ask the human at these moments:

- Before turning a plan into a full spec, if scope is unclear.
- Before implementation, after the spec is written.
- After review passes, so the human can test manually.
- Before archive/push, if the project requires release confirmation.

## Failure Behavior

If implementation fails:

- Executor records the failing command and error summary.
- Orchestrator sends the failure to Reviewer if the spec may need clarification.
- Otherwise Executor fixes and recommits.

If review fails:

- Reviewer writes concrete required fixes.
- Executor fixes based on those notes.
- Reviewer reviews again.

If human testing fails:

- Reviewer translates human feedback into spec/task updates.
- Executor fixes and commits.
- Reviewer reviews again before another human test.

## Origin

This loop was extracted from a real Codex/OpenSpec development workflow using:

- One Orchestrator thread
- Planner, Executor, and Reviewer role threads
- Heartbeat polling
- Persistent `.agent-loop/state.md`
