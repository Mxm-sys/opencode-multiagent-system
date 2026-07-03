# OpenCode 多智能体协同系统 — 决策层

## 当前阶段：决策层

本项目采用渐进式构建。当前已完成**决策层**（三学士献计），执行层待后续建立。

## 决策层架构

```
用户需求 → Presider → [Architect甲 / Architect乙 / Architect丙] → Judge → 胜出方案 → (执行层)
```

## Agent 角色

| Agent | 角色 | 模型 | 权限 | 说明 |
|-------|------|------|------|------|
| **presider** | 主持者（入口） | Claude Sonnet 4 | 只读 | 接收需求、调度流程、输出结果 |
| **architect_alpha** | 学士甲 | Claude Sonnet 4 | 只读 | 独立产出方案 |
| **architect_beta** | 学士乙 | Claude Sonnet 4 | 只读 | 独立产出方案 |
| **architect_gamma** | 学士丙 | Claude Sonnet 4 | 只读 | 独立产出方案 |
| **judge** | 裁决者 | Claude Sonnet 4 | 只读 | 对比评估、选定最优 |

> 三个 Architect 使用**完全相同的提示词**（`agents/decision/architect/prompt.md`），仅 agent key 不同。

## 核心流程

1. **Presider** 接收用户需求，准备上下文
2. 将同一需求分派给 **alpha / beta / gamma** 三个 Architect 并行处理
3. 三个 Architect 各自独立输出方案 JSON（互不通信）
4. **Judge** 审阅三份方案，按七维度打分，输出裁决书
5. **Presider** 汇总输出胜出方案，移交执行层

## 快速开始

```bash
# 以 presider 作为入口 Agent 启动
opencode --agent presider
```

## 项目结构

```
opencode-multiagent-system/
├── opencode.json                          # 主配置（5 个 Agent + 1 个 Skill）
├── AGENTS.md                              # 本文件
├── agents/decision/
│   ├── presider/prompt.md                 # 主持者提示词
│   ├── architect/prompt.md                # 三学士共用提示词
│   └── judge/prompt.md                    # 裁决者提示词
├── skills/
│   └── proposal-competition/skill.md      # 三学士献计流程
├── workflows/
│   └── decision-flow.md                   # 决策层工作流
└── .opencode/rules.md                     # 项目规则
```