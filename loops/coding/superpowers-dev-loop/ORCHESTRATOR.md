# Superpowers Dev Loop — Orchestrator Protocol

This file defines how the Agent manages the Skill Stack.

On every user message or heartbeat wakeup, the Agent must read:

1. `.agent-loop/ORCHESTRATOR.md`
2. `.agent-loop/state.md`

Do not rely on conversation memory. Use these files to determine current skill and advance the workflow.

## Core Principles

- The Agent follows the Skill Stack in order. No skill is skipped.
- Before responding, the Agent checks: does any skill in the stack apply right now? If there is even 1% chance a skill applies, invoke it.
- At most one Subagent modifies project files at a time.
- Subagents are fresh per task — no context carried between them.
- Persist workflow state in `.agent-loop/state.md`.
- Pause heartbeat at human checkpoints.

## Skill Stack (ordered)

1. **Brainstorming** — explore context, clarify, propose approaches, write design doc.
2. **Using Git Worktrees** — create isolated workspace, run setup, verify test baseline.
3. **Writing Plans** — break approved design into micro-tasks, write plan doc.
4. **Subagent-Driven Development** — dispatch Subagent per task with TDD + two-stage review.
5. **Requesting Code Review** — final code review against plan.
6. **Finishing a Development Branch** — full test suite, present options, cleanup.

## Skill Transitions

### Brainstorming → Using Git Worktrees

Trigger: human approves design document.

The Agent:
- Sets skill to `using-git-worktrees` in state.
- Resets heartbeat to 3 minutes.

### Using Git Worktrees → Writing Plans

Trigger: worktree is created, setup complete, baseline tests pass.

The Agent:
- Records worktree path in state.
- Sets skill to `writing-plans`.
- Resets heartbeat to 3 minutes.

### Writing Plans → Subagent-Driven Development

Trigger: human approves implementation plan.

The Agent:
- Saves plan to `docs/superpowers/plans/`.
- Sets skill to `subagent-driven-development`.
- Resets heartbeat to 10 minutes.
- Offers human two execution options: Subagent-Driven or Inline Execution.

### Subagent-Driven Development → Requesting Code Review

Trigger: all tasks in the plan are complete and reviewed (two-stage pass for each).

The Agent:
- Sets skill to `requesting-code-review`.
- Resets heartbeat to 5 minutes.

### Requesting Code Review → Finishing a Development Branch

Trigger: final code review passes with no critical issues.

The Agent:
- Sets skill to `finishing-a-development-branch`.
- Resets heartbeat to 5 minutes.

### Finishing a Development Branch → Done

Trigger: human chooses an option (merge / PR / keep / discard).

The Agent:
- Executes the chosen action.
- Cleans up worktree if merge or discard.
- Optionally asks if human wants to start the next feature.

## Heartbeat Rules

| Skill | Active Role | Waiting for Human | Heartbeat |
|---|---|---|---|
| Brainstorming | agent | false | ACTIVE, 3 min |
| Using Git Worktrees | agent | false | ACTIVE, 3 min |
| Writing Plans | agent | false | ACTIVE, 3 min |
| Subagent-Driven Development | subagent | false | ACTIVE, 10 min |
| Requesting Code Review | subagent | false | ACTIVE, 5 min |
| Finishing a Development Branch | agent | false | ACTIVE, 5 min |
| Human checkpoint | agent | true | PAUSED |

## Heartbeat Wakeup Behavior

On heartbeat wakeup:

1. Read `.agent-loop/ORCHESTRATOR.md` and `.agent-loop/state.md`.
2. If waiting for human is `true`, ensure heartbeat is paused and do not advance.
3. If a Subagent is running, check its status.
4. If Subagent finished, run two-stage review, then advance to next task or next skill.
5. If no Subagent is running and current skill has unstarted work, start the next step.
6. Update state and heartbeat interval after each transition.

## Human Checkpoints

- **Design approval**: after brainstorming, before creating worktree.
- **Plan approval**: after writing plans, before execution.
- **Branch finish**: after finishing branch, before cleanup.

## Subagent Dispatch Contract

When dispatching a Subagent for a task, include:

- Task description from the plan
- Exact file paths
- Expected code behavior
- Test expectations
- Verification commands

When a Subagent completes, record:

- Task completed
- Commit hash
- Files changed
- Tests run and results
- Review findings (spec compliance + code quality)

## Artifact Locations

- Design docs: `docs/superpowers/specs/YYYY-MM-DD--<feature>.md`
- Plan docs: `docs/superpowers/plans/YYYY-MM-DD--<feature>.md`
- Worktree: platform-native path or `~/.config/superpowers/worktrees/<project>/<branch>`
