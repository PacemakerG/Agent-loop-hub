# Agent Loop Hub

[English](README.md) | [中文](README.zh-CN.md)

Agent Loop Hub is a community collection of reusable AI Agent workflow loops.

## Description

Agent Loop Hub collects practical, reusable workflow templates that show how AI agents plan, execute, review, recover from failure, and hand control back to humans. Instead of sharing a single prompt, each loop describes the roles, state, checkpoints, and repeatable process behind an agent-powered workflow.

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

## Loop Gallery

| Category | Loop | Use Case | Status |
|---|---|---|---|
| Coding | [OpenSpec Dev Loop](loops/coding/openspec-dev-loop/README.md) | Plan -> Spec -> Code -> Review -> Test -> Archive | Ready |
| Coding | [Superpowers Dev Loop](loops/coding/superpowers-dev-loop/README.md) | Brainstorm -> Plan -> Subagent TDD -> Review -> Finish | Ready |
| Research | [Deep Research Loop](loops/research/deep-research-loop/README.md) | Search -> Read -> Synthesize -> Source Check -> Report | Planned |
| Writing | [Content Creator Loop](loops/writing/content-creator-loop/README.md) | Research -> Outline -> Draft -> Critique -> Revise | Planned |
| Productivity | [Meeting Assistant Loop](loops/productivity/meeting-assistant-loop/README.md) | Transcript -> Summary -> Action Items -> Follow-up | Planned |
| Business | [Lead Scoring Loop](loops/business/lead-scoring-loop/README.md) | Collect -> Enrich -> Score -> Human Review -> CRM Update | Planned |
| Data | [Data Analysis Loop](loops/data/data-analysis-loop/README.md) | Load -> Clean -> Analyze -> Visualize -> Report | Planned |

Choose **OpenSpec Dev Loop** for lightweight coding workflows.
Choose **Superpowers Dev Loop** for stricter, TDD-first, worktree-isolated development.

## Repository Structure

```text
agent-loop-hub/
  README.md
  README.zh-CN.md
  loops/
    coding/
      openspec-dev-loop/
        README.md
        loop.yaml
        template/
          ORCHESTRATOR.md
          state.template.md
          prompts/
            planner.prompt.md
            executor.prompt.md
            reviewer.prompt.md
      superpowers-dev-loop/
        README.md
        loop.yaml
        template/
          ORCHESTRATOR.md
          state.template.md
          prompts/
            brainstorming.prompt.md
            writing-plans.prompt.md
            subagent-driven-development.prompt.md
            requesting-code-review.prompt.md
            finishing-a-development-branch.prompt.md
    research/
      deep-research-loop/
        README.md
        loop.yaml
        template/
          ORCHESTRATOR.md
          state.template.md
          prompts/
    writing/
      content-creator-loop/
        README.md
        loop.yaml
        template/
          ORCHESTRATOR.md
          state.template.md
          prompts/
    productivity/
      meeting-assistant-loop/
        README.md
        loop.yaml
        template/
          ORCHESTRATOR.md
          state.template.md
          prompts/
    business/
      lead-scoring-loop/
        README.md
        loop.yaml
        template/
          ORCHESTRATOR.md
          state.template.md
          prompts/
    data/
      data-analysis-loop/
        README.md
        loop.yaml
        template/
          ORCHESTRATOR.md
          state.template.md
          prompts/
  schemas/
    loop.schema.yaml
  ATTRIBUTIONS.md
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
