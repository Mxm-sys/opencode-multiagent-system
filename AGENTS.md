# OpenCode 多智能体协同系统

## 项目概述

本项目是基于 OpenCode 构建的多智能体协同开发系统。通过定义多个专用 Agent 和协作工作流，实现类似"AI 开发团队"的协作模式。

## Agent 角色

| Agent | 角色定位 | 模型 | 工具权限 |
|-------|----------|------|----------|
| **orchestrator** | 团队协调者 | Claude Sonnet 4 | 只读 + 搜索 |
| **developer** | 开发者 | Claude Sonnet 4 | 读写 + 执行 |
| **reviewer** | 代码审查者 | Claude Sonnet 4 | 只读 |
| **researcher** | 技术调研者 | GPT-4o | 只读 |
| **tester** | 测试工程师 | Claude Sonnet 4 | 读写 + 执行 |
| **documenter** | 文档工程师 | GPT-4o | 读写 |

## 协作流程

1. 通过 `orchestrator` 入口提交任务
2. Orchestrator 使用 `task-planning` skill 制定计划
3. 按需分派给 `researcher` / `developer` / `tester`
4. 所有代码变更经 `reviewer` 审查
5. 最终由 `documenter` 更新文档

## 快速开始

```bash
# 进入项目目录
cd opencode-multiagent-system

# 启动 OpenCode（指定 orchestrator 作为入口 Agent）
opencode --agent orchestrator
```

## 配置说明

主配置文件 `opencode.json` 定义了所有 Agent 和 Skills。你可以根据需要：

- 修改每个 Agent 使用的模型
- 调整 Agent 的工具权限
- 添加新的 Skill
- 配置 MCP 服务器

## 项目结构

```
opencode-multiagent-system/
├── opencode.json               # 主配置文件
├── AGENTS.md                   # 本文件 - Agent 说明文档
├── agents/                     # Agent 系统提示词
│   ├── orchestrator/prompt.md
│   ├── developer/prompt.md
│   ├── reviewer/prompt.md
│   ├── researcher/prompt.md
│   ├── tester/prompt.md
│   └── documenter/prompt.md
├── skills/                     # 自定义 Skills
│   ├── task-planning/skill.md
│   ├── code-review/skill.md
│   ├── test-generation/skill.md
│   ├── documentation/skill.md
│   └── research/skill.md
├── workflows/                  # 协作工作流定义
│   ├── development-flow.md
│   └── review-flow.md
├── .opencode/                  # OpenCode 项目配置
│   └── rules.md
└── .github/workflows/          # GitHub Actions
    └── opencode.yml
```