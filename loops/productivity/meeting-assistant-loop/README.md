# Meeting Assistant Loop

**Status:** Planned

For meeting minutes, action item extraction, task sync, and post-meeting follow-up.

## Flow

```text
Transcript → Clean Notes → Summary → Action Items → Owner Mapping → Tool Sync → Follow-up Draft
```

## Roles

### Transcript Cleaner
- Clean raw transcript, remove filler, identify speakers.

### Summarizer
- Produce a concise meeting summary.

### Action Item Extractor
- Identify tasks, owners, and deadlines.

### Task Dispatcher
- Map action items to tools (Trello, Slack, Jira, etc.).

### Follow-up Writer
- Draft follow-up message for attendees.

## Human Checkpoints

- Approve action items
- Approve follow-up message

## Source / Attribution

- **Type**: inspired_by
- **Name**: CrewAI Meeting Assistant Flow
- **URL**: https://github.com/crewAIInc/crewAI-examples
- **License**: please verify
- **Notes**: Inspired by CrewAI Meeting Assistant Flow, which processes meeting notes and integrates with Trello/Slack. This is an original Agent Loop Hub abstraction.

## TODO

- [ ] Write `template/ORCHESTRATOR.md`
- [ ] Write `template/state.template.md`
- [ ] Write prompts for each role
- [ ] Add heartbeat configuration
- [ ] Add failure behavior
