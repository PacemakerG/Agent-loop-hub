# Agent Loop Hub

[English](README.md) | [中文](README.zh-CN.md)

Agent Loop Hub 是一个收集可复用 AI Agent 工作流模板的开源仓库。

## 项目简介

Agent Loop Hub 收集的是一套套可以复用的 Agent 工作流：Agent 怎么规划、怎么执行、怎么 review、失败后怎么修、什么时候把控制权交还给人。它不是分享单个 Prompt，而是分享“Agent 如何循环干活”的完整方法。

大家以前分享 Prompt，这个仓库分享 Agent 怎么循环干活。

换句话说，这里收集的不是一句提示词，而是一套完整的工作方式：谁先规划，谁去执行，谁来 review，什么时候停下来问人，状态存在哪里，失败以后怎么继续。

> People share prompts. We share loops.

## 什么是 Agent Loop？

Agent Loop 是一种可以反复复用的 Agent 工作流模式。

它回答这些问题：

- 谁负责规划？
- 谁负责执行？
- 谁负责 review？
- 人什么时候介入？
- 状态存在哪里？
- 失败以后怎么恢复和继续？

## Loop Gallery

| 分类 | Loop | 适用场景 | 状态 |
|---|---|---|---|
| Coding | [OpenSpec Dev Loop](loops/coding/openspec-dev-loop/README.md) | Plan -> Spec -> Code -> Review -> Test -> Archive | Ready |

## 第一个 Loop

### OpenSpec Dev Loop

这是一个面向软件开发的 Planner-Executor-Reviewer 工作流。

它适合这种开发方式：

- Planner：把需求拆成计划和 OpenSpec change。
- Executor：只按已经通过的 spec 写代码和提交。
- Reviewer：检查实现是否符合 spec，把问题打回去修。

流程：

```text
Plan -> Spec -> Implement -> Review -> Human Test -> Fix -> Archive
```

从这里开始看：

- [OpenSpec Dev Loop](loops/coding/openspec-dev-loop/README.md)
- [Loop metadata](loops/coding/openspec-dev-loop/loop.yaml)
- [中文原始模板](loops/coding/openspec-dev-loop/AGENT_LOOP_TEMPLATE.md)
- [Orchestrator 协议](loops/coding/openspec-dev-loop/ORCHESTRATOR.md)
- [状态模板](loops/coding/openspec-dev-loop/state.template.md)

## 仓库结构

```text
agent-loop-hub/
  README.md
  README.zh-CN.md
  loops/
    coding/
      openspec-dev-loop/
        README.md
        loop.yaml
        AGENT_LOOP_TEMPLATE.md
        ORCHESTRATOR.md
        state.template.md
        planner.prompt.md
        executor.prompt.md
        reviewer.prompt.md
    writing/
    research/
    data/
  schemas/
    loop.schema.yaml
  CONTRIBUTING.md
  LICENSE
```

## 什么内容适合放进来？

这里收集的是完整 loop，不是单个 prompt。

一个好的 loop 应该说明：

- 有哪些角色
- 每个角色负责什么
- 流程怎么推进
- 人在哪些节点介入
- 状态怎么保存
- 失败以后怎么修、怎么继续
- 每个角色可以直接复用的 prompt 模板

## License

MIT
