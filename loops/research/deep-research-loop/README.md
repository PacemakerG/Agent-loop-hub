# Deep Research Loop

**Status:** Planned

For in-depth research, information gathering, cross-validation, and generating research reports with citations.

## Flow

```text
Question → Search Plan → Web/Doc Search → Read & Extract → Synthesize → Source Check → Human Review → Final Report
```

## Roles

### Research Planner
- Understand the question, break it into sub-questions, plan search strategy.

### Searcher
- Execute searches across web, docs, or databases.

### Reader
- Read and extract relevant content from each source.

### Synthesizer
- Combine findings into a coherent draft with citations.

### Source Reviewer
- Verify accuracy, relevance, and citation quality.

## Human Checkpoints

- Approve research plan
- Review final report

## Source / Attribution

- **Type**: inspired_by
- **Name**: LangGraph examples / CrewAI examples
- **URL**: https://github.com/langchain-ai/langgraph/tree/main/examples, https://github.com/crewAIInc/crewAI-examples
- **License**: please verify
- **Notes**: Inspired by public research, RAG, plan-and-execute, and report-generation examples. This loop is an original Agent Loop Hub abstraction.

## TODO

- [ ] Write `template/ORCHESTRATOR.md`
- [ ] Write `template/state.template.md`
- [ ] Write prompts for each role
- [ ] Add heartbeat configuration
- [ ] Add failure behavior
