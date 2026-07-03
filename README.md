# OpenCode 多智能体协同系统

基于 [OpenCode](https://opencode.ai) 构建的多智能体 (Multi-Agent) 协同开发系统。通过定义多个专用 Agent 和标准化协作工作流，将单个 AI 编程会话升级为完整的"AI 开发团队"。

## 系统架构

```
                   ┌─────────────────────────────────────────┐
                   │           Orchestrator (协调者)          │
                   │  负责任务分解、Agent 分派、结果整合      │
                   └──────┬──────┬──────┬──────┬──────┬──────┘
                          │      │      │      │      │
              ┌───────────┤      │      │      │      ├───────────┐
              ▼                  ▼      ▼      ▼                  ▼
     ┌──────────────┐  ┌──────────┐ ┌──────┐ ┌────────┐  ┌────────────┐
     │  Researcher  │  │ Developer│ │Tester│ │Reviewer│  │ Documenter │
     │  (调研者)    │  │ (开发者) │ │(测试)│ │(审查者)│  │  (文档)    │
     └──────────────┘  └──────────┘ └──────┘ └────────┘  └────────────┘
```

## Agent 角色

| Agent | 职责 | 模型 | 权限 |
|-------|------|------|------|
| **Orchestrator** | 协调者：任务分解、智能分派、进度管理 | Claude Sonnet 4 | 只读 |
| **Developer** | 开发者：编码实现、Bug 修复、功能开发 | Claude Sonnet 4 | 读写 + 执行 |
| **Reviewer** | 审查者：代码质量、安全审计、规范检查 | Claude Sonnet 4 | 只读 |
| **Researcher** | 调研者：技术调研、方案对比、信息收集 | GPT-4o | 只读 |
| **Tester** | 测试者：测试编写、覆盖率分析、质量验证 | Claude Sonnet 4 | 读写 + 执行 |
| **Documenter** | 文档者：项目文档、API 文档、变更日志 | GPT-4o | 读写 |

## Skills

| Skill | 用途 |
|-------|------|
| **task-planning** | 任务分解、依赖分析、资源分配 |
| **code-review** | 多维度代码审查（功能/安全/性能/质量） |
| **test-generation** | 自动生成测试用例（单元/集成） |
| **documentation** | 文档生成和维护 |
| **research** | 技术调研和方案对比 |

## 快速开始

### 前置条件

- 安装 [OpenCode](https://opencode.ai/docs)
- 配置 API Key（Anthropic / OpenAI）

### 使用

```bash
# 1. 克隆项目
git clone https://github.com/your-username/opencode-multiagent-system.git
cd opencode-multiagent-system

# 2. 启动 OpenCode，以 orchestrator 作为入口 Agent
opencode --agent orchestrator
```

### 在 GitHub Issues/PR 中使用

在仓库评论中输入 `/opencode` 或 `/multiagent` 即可触发 OpenCode 自动处理。

需要先在 GitHub 仓库中配置 `ANTHROPIC_API_KEY` 和 `OPENAI_API_KEY` 为 Actions Secrets。

## 自定义配置

### 添加新的 Agent

在 `opencode.json` 的 `agent` 字段中添加：

```json
"your-agent": {
  "model": "provider/model-name",
  "prompt": "file://agents/your-agent/prompt.md",
  "tools": {
    "read": true,
    "edit": true,
    "write": true,
    "bash": false
  }
}
```

### 修改模型

每个 Agent 可以独立指定模型提供商和模型，支持：
- `anthropic/claude-sonnet-4-20250514`
- `openai/gpt-4o`
- `google/gemini-2.0-flash`
- 及所有 OpenCode 支持的模型

## 项目结构

```
opencode-multiagent-system/
├── opencode.json                # OpenCode 主配置（Agent/Skill/MCP 定义）
├── AGENTS.md                    # Agent 说明文档（OpenCode 自动读取）
├── agents/                      # Agent 系统提示词
│   ├── orchestrator/prompt.md
│   ├── developer/prompt.md
│   ├── reviewer/prompt.md
│   ├── researcher/prompt.md
│   ├── tester/prompt.md
│   └── documenter/prompt.md
├── skills/                      # 自定义 Skills
│   ├── task-planning/skill.md
│   ├── code-review/skill.md
│   ├── test-generation/skill.md
│   ├── documentation/skill.md
│   └── research/skill.md
├── workflows/                   # 协作工作流定义
│   ├── development-flow.md
│   └── review-flow.md
├── .opencode/rules.md           # 项目协作规则
├── .github/workflows/           # GitHub Actions
│   └── opencode.yml
└── examples/                    # 示例配置
    └── basic-setup/opencode.json
```

## License

MIT