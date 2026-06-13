# Agent Loop Hub

Agent Loop Hub is a community collection of reusable AI Agent workflow loops.

Most people share prompts.
This repo shares loops.

A loop defines how agents repeatedly plan, act, review, fix, and hand control back to humans when needed.

> People share prompts. We share loops.

## What Is An Agent Loop?

An Agent Loop is a reusable workflow pattern for AI agents.

It answers:

- Who plans?
- Who executes?
- Who reviews?
- When should the human step in?
- Where is state stored?
- How does the workflow continue after failure?

## First Loop

### OpenSpec Dev Loop

A Planner-Executor-Reviewer loop for semi-automated software development with human checkpoints.

A software development loop with three roles:

- Planner: writes plans and OpenSpec changes.
- Executor: implements code based on approved specs.
- Reviewer: reviews the diff and sends fixes back.

Flow:

```text
Plan -> Spec -> Implement -> Review -> Human Test -> Fix -> Archive
```

Start here:

- [OpenSpec Dev Loop](loops/openspec-dev-loop/README.md)
- [Original Chinese template](loops/openspec-dev-loop/AGENT_LOOP_TEMPLATE.md)
- [Orchestrator protocol](loops/openspec-dev-loop/ORCHESTRATOR.md)
- [State template](loops/openspec-dev-loop/state.template.md)

## Repository Structure

```text
agent-loop-hub/
  README.md
  loops/
    openspec-dev-loop/
      README.md
      AGENT_LOOP_TEMPLATE.md
      ORCHESTRATOR.md
      state.template.md
      planner.prompt.md
      executor.prompt.md
      reviewer.prompt.md
  schemas/
    loop.schema.yaml
  CONTRIBUTING.md
  LICENSE
```

## What Belongs Here?

This repository is for complete agent workflow loops, not one-off prompts.

A good loop should include:

- Role definitions
- Execution flow
- Human checkpoints
- State persistence rules
- Failure and retry behavior
- Prompt templates for each role

## License

MIT
