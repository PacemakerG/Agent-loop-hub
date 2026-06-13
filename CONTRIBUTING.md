# Contributing

Thanks for helping build Agent Loop Hub.

This repository collects reusable AI Agent workflow loops.

## What To Submit

Submit loops, not isolated prompts.

A loop should explain:

- Who plans
- Who executes
- Who reviews
- Where state is stored
- When humans step in
- How failure, retry, and continuation work

## Loop Directory Format

Create a directory under the matching category:

```text
loops/<category>/<your-loop-slug>/
  loop.yaml
  README.md
  ORCHESTRATOR.md
  state.template.md
  planner.prompt.md
  executor.prompt.md
  reviewer.prompt.md
```

Your loop may use different role names. If it does, name the prompt files after your roles.

Recommended categories:

- `coding`
- `writing`
- `research`
- `data`

## Loop Metadata

Each loop should include a `loop.yaml` file:

```yaml
name: OpenSpec Dev Loop
category: coding
description: Planner-Executor-Reviewer loop for OpenSpec-driven software development.
roles:
  - Planner
  - Executor
  - Reviewer
human_checkpoints:
  - plan_review
  - spec_review
  - manual_test
state_file: .agent-loop/state.md
```

This metadata lets future websites, search pages, and generated galleries index loops automatically.

## Guidelines

- Keep loops practical and reproducible.
- Include clear stop conditions for every role.
- Include human checkpoints.
- Include state persistence rules.
- Include `loop.yaml`.
- Avoid secrets, private thread IDs, private repository names, or personal tokens.
- Prefer small loops that people can adapt quickly.

## Review Criteria

Maintainers will look for:

- Clear workflow
- Clear role boundaries
- Safe human handoff
- Repeatable state model
- Useful failure behavior

## Motto

People share prompts. We share loops.
