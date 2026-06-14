# Superpowers Dev Loop

A skill-stack-driven development loop inspired by the [Superpowers](https://github.com/obra/superpowers) framework. It enforces a complete software development workflow — brainstorm first, plan in micro-tasks, execute with TDD via subagents, review in two stages, and finish the branch with structured options.

## When to Use This Loop

**Best for:**
- 大功能开发
- 重构
- 核心逻辑改动
- 需要 TDD 的任务
- 需要 git worktree 隔离的任务
- 高纪律、强流程的软件开发

**Not ideal for:**
- 小 bug
- 文案修改
- 简单样式调整
- 小配置改动
- 一次性脚本
- 不需要测试保护的小改动

## Core Idea

Instead of dispatching separate role agents (Planner, Executor, Reviewer), the Superpowers model puts **one Agent** in control of a **Skill Stack**. The agent checks which skill applies, invokes it, produces artifacts, and advances to the next skill when the current one is complete.

The skills are mandatory checkpoints, not suggestions. The agent does not skip phases.

## Roles

### Agent

The Agent is the single main coding agent that manages the entire workflow. It:

- Follows the Skill Stack in order.
- Invokes the right skill at the right time.
- Dispatches Subagents during the execution phase.
- Manages state, heartbeats, and human checkpoints.

### Subagent

A temporary agent dispatched by the Agent during the **Subagent-Driven Development** skill. Each Subagent:

- Gets one micro-task from the plan.
- Follows RED-GREEN-REFACTOR discipline.
- Runs tests and commits the result.
- Is discarded after the task is reviewed and accepted.

## Skill Stack (Flow)

```text
Brainstorming
  → produce design doc
  → HUMAN CHECKPOINT: approve design
  →
Using Git Worktrees
  → create isolated workspace
  →
Writing Plans
  → produce micro-task plan (2–5 min per task)
  → HUMAN CHECKPOINT: approve plan
  →
Subagent-Driven Development  (per task: RED→GREEN→REFACTOR)
  → Requesting Code Review (two-stage: spec compliance → code quality)
  → loop until all tasks done
  →
Finishing a Development Branch
  → full test suite, final review
  → HUMAN CHECKPOINT: merge / PR / keep / discard
  → clean up worktree
```

Expanded:

```text
Agent explores project context, asks clarifying questions, proposes approaches
  →
Agent writes design document to docs/superpowers/specs/
  →
Human approves design
  →
Agent creates isolated worktree (native tool or git worktree), runs setup, verifies test baseline
  →
Agent writes micro-task plan to docs/superpowers/plans/
  →
Human approves plan
  →
For each task in plan:
  Agent dispatches a fresh Subagent
  Subagent: write failing test → watch it fail → write minimal code → watch it pass → refactor → commit
  Agent dispatches Spec Reviewer Subagent: does code match spec?
    If no → Subagent fixes spec gaps
  Agent dispatches Code Quality Reviewer Subagent: is code well-built?
    If no → Subagent fixes quality issues
  Mark task complete
  →
Agent runs full test suite
Agent dispatches final Code Review Subagent
Agent presents options: merge locally / push and create PR / keep branch / discard worktree
  →
Human chooses action
  →
Agent cleans up worktree
```

## Human Checkpoints

- **Design approval**: before any code is written, the human must approve the design document.
- **Plan approval**: before execution begins, the human must approve the micro-task plan.
- **Branch finish**: after all tasks are done, the human chooses merge / PR / keep / discard.

## Project Files

Add these to the target project:

```text
.agent-loop/
  ORCHESTRATOR.md
  state.md
```

And create these directories for artifacts:

```text
docs/superpowers/
  specs/     ← design documents from brainstorming
  plans/     ← implementation plans from writing plans
```

## Template Files

- `template/ORCHESTRATOR.md`
- `template/state.template.md`
- `template/prompts/brainstorming.prompt.md`
- `template/prompts/writing-plans.prompt.md`
- `template/prompts/subagent-driven-development.prompt.md`
- `template/prompts/requesting-code-review.prompt.md`
- `template/prompts/finishing-a-development-branch.prompt.md`

## Heartbeat

Suggested intervals per skill:

| Skill | Interval |
|---|---|
| Brainstorming | 3 minutes |
| Writing Plans | 3 minutes |
| Subagent-Driven Development | 10 minutes |
| Requesting Code Review | 5 minutes |
| Finishing Branch | 5 minutes |
| Human checkpoint | paused |

## Failure Behavior

If brainstorming fails to produce a clear design:
- Agent asks more targeted questions.
- Agent proposes simpler alternatives.

If worktree creation fails:
- Agent falls back to in-place development (sandbox mode).

If Subagent execution fails:
- Agent captures error, diagnoses, adjusts plan if needed, retries.

If review finds critical issues:
- Subagent fixes, reviewer rechecks, task is blocked until resolved.

If finishing step fails (test suite red):
- Agent reports failures, offers to fix or abort.

## Source / Attribution

- **Type**: original
- **Notes**: Original Agent Loop Hub design for Superpowers-style skill-stack development. Designed around the Superpowers workflow concept (brainstorming → git worktrees → writing plans → subagent TDD → code review → finishing branch), but all prompts, templates, and loop structure are original to Agent Loop Hub.
