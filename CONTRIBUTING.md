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
  README.md
  loop.yaml
  template/
    ORCHESTRATOR.md
    state.template.md
    prompts/
      <role>.prompt.md
      <role>.prompt.md
      ...
```

The loop root directory keeps only `README.md` and `loop.yaml`. All files meant to be copied into a target project go under `template/`. Prompt files for each role go under `template/prompts/`.

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

## Attribution Requirements

Every loop **must** include a `source` field in `loop.yaml` and a `Source / Attribution` section in `README.md`.

When submitting a loop, answer these questions:

1. Is this loop **original** (designed from scratch)?
2. Is it **inspired by** another project or workflow?
3. Is it **adapted from** an existing template or codebase?
4. If adapted or inspired, what is the original URL, project name, and license?
5. Which parts were rewritten, abstracted, or directly referenced?

If unsure about the original project's license, write `license: unknown / please verify`.

## Guidelines

- Keep loops practical and reproducible.
- Include clear stop conditions for every role.
- Include human checkpoints.
- Include state persistence rules.
- Include `loop.yaml` with a valid `source` field.
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
