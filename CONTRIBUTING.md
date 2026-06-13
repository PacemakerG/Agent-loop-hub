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

Create a directory under `loops/`:

```text
loops/<your-loop-slug>/
  README.md
  ORCHESTRATOR.md
  state.template.md
  planner.prompt.md
  executor.prompt.md
  reviewer.prompt.md
```

Your loop may use different role names. If it does, name the prompt files after your roles.

## Guidelines

- Keep loops practical and reproducible.
- Include clear stop conditions for every role.
- Include human checkpoints.
- Include state persistence rules.
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
