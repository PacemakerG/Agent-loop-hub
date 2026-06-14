# Data Analysis Loop

**Status:** Planned

For data cleaning, exploratory analysis, visualization, insight generation, and report creation.

## Flow

```text
Load Data → Validate Schema → Clean Data → Explore → Analyze → Visualize → Insight Review → Final Report
```

## Roles

### Data Loader
- Load data from files, databases, or APIs.

### Data Cleaner
- Validate schema, handle missing values, fix inconsistencies.

### Analyst
- Perform statistical analysis, hypothesis testing, and feature exploration.

### Visualization Agent
- Generate charts and dashboards for key findings.

### Insight Reviewer
- Review findings for accuracy and business relevance.

## Human Checkpoints

- Confirm analysis goal
- Review final insights

## Source / Attribution

- **Type**: inspired_by
- **Name**: CrewAI Stock Analysis / LangGraph RAG and analysis examples
- **URL**: https://github.com/crewAIInc/crewAI-examples, https://github.com/langchain-ai/langgraph/tree/main/examples
- **License**: please verify
- **Notes**: Inspired by public agent analysis examples. This loop should be platform-agnostic and not copy framework-specific code.

## TODO

- [ ] Write `template/ORCHESTRATOR.md`
- [ ] Write `template/state.template.md`
- [ ] Write prompts for each role
- [ ] Add heartbeat configuration
- [ ] Add failure behavior
