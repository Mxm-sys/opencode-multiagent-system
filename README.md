# OpenCode 多智能体协同系统

基于 [OpenCode](https://opencode.ai) 构建的多智能体协同开发系统。

## 当前阶段：决策层（三学士献计）

采用渐进式构建，当前已完成**决策层**：对同一需求并行启动三个 Architect 智能体各自独立产出方案，再由 Judge 裁决选定最优方案。

```
用户需求
    │
    ├──→ Architect 甲 ──→ proposal_alpha
    ├──→ Architect 乙 ──→ proposal_beta
    └──→ Architect 丙 ──→ proposal_gamma
                              │
                     Judge 裁决
                              │
                              ▼
                    胜出方案 → 移交执行层
```

## Agent 角色

| Agent | 角色 | 权限 | 职责 |
|-------|------|------|------|
| **presider** | 主持者 | 只读 | 入口 Agent，调度决策流程 |
| **architect_alpha** | 学士甲 | 只读 | 独立产出方案 |
| **architect_beta** | 学士乙 | 只读 | 独立产出方案 |
| **architect_gamma** | 学士丙 | 只读 | 独立产出方案 |
| **judge** | 裁决者 | 只读 | 七维度打分，选定最优 |

## 快速开始

```bash
# 安装 OpenCode 后
cd opencode-multiagent-system
opencode --agent presider
```

## 为什么"三方案择优"

- **成本可控**：设计阶段 3 倍思考，执行阶段仍 1 倍，总成本 ~5x 而非 9x
- **设计多样性**：同一需求可能得到缓存、异步、重试等完全不同思路，择优比单次抽奖可靠
- **避免合并灾难**：只选一个方案执行，不需要合并三份代码 diff

## 项目结构

```
├── opencode.json                    # 主配置
├── AGENTS.md                        # Agent 文档
├── agents/decision/
│   ├── presider/prompt.md           # 主持者
│   ├── architect/prompt.md          # 三学士共用
│   └── judge/prompt.md              # 裁决者
├── skills/proposal-competition/     # 献计流程 Skill
├── workflows/decision-flow.md       # 决策工作流
└── .opencode/rules.md               # 项目规则
```

## 后续规划

- [ ] 执行层：Operator（照方案编码）、Tester（测试验证）、Reviewer（代码审查）
- [ ] 协作层：Agent 间的上下文传递和状态管理
- [ ] 更多 Skills 和工作流

## License

MIT