# Lead Scoring Loop

**Status:** Planned

For sales lead collection, profile enrichment, scoring, human review, and CRM updates.

## Flow

```text
Collect Lead → Enrich Profile → Score Lead → Explain Score → Human Review → CRM Update → Follow-up Suggestion
```

## Roles

### Lead Collector
- Gather leads from sources (forms, import, API, etc.).

### Enricher
- Enrich lead profile with public data (company, title, industry, etc.).

### Scorer
- Score lead based on defined criteria and models.

### Reviewer
- Review high-value or uncertain leads before action.

### CRM Updater
- Update CRM records and suggest next actions.

## Human Checkpoints

- Review high-value or uncertain leads
- Approve CRM update

## Source / Attribution

- **Type**: inspired_by
- **Name**: CrewAI Lead Score Flow
- **URL**: https://github.com/crewAIInc/crewAI-examples
- **License**: please verify
- **Notes**: Inspired by CrewAI Lead Score Flow, especially the human-in-the-loop review pattern. Do not copy implementation or prompts.

## TODO

- [ ] Write `template/ORCHESTRATOR.md`
- [ ] Write `template/state.template.md`
- [ ] Write prompts for each role
- [ ] Add heartbeat configuration
- [ ] Add failure behavior
