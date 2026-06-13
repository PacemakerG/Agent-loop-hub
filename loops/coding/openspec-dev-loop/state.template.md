# <Project Name> Agent Loop State

## Role Threads

- Orchestrator: <current-thread-or-agent>
- Planner: <planner-thread-id-or-agent-name>
- Executor: <executor-thread-id-or-agent-name>
- Reviewer: <reviewer-thread-id-or-agent-name>

## Current State

- Phase: <phase>
- Current change: <change-id-or-none>
- Active role: <orchestrator|planner|executor|reviewer>
- Waiting for human: <true|false>
- Heartbeat id: <automation-id-or-none>
- Heartbeat interval: <paused|3 minutes|5 minutes|10 minutes>

## Phase Intervals

- planner_reviewing_plan: 3 minutes
- planner_writing_spec: 3 minutes
- executor_implementing: 10 minutes
- executor_fixing: 10 minutes
- reviewer_reviewing: 5 minutes
- reviewer_updating_spec: 5 minutes
- waiting_human_*: paused

## Current Todo

- <next-action>

## Latest Result

- Summary: <short-summary>
- Files changed: <files-or-none>
- Commits: <commit-hashes-or-none>
- Tests: <commands-and-results-or-none>
- Blockers: <blockers-or-none>
