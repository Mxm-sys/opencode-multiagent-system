# 项目规则

## 通用规则

1. 所有代码变更必须先经过 review
2. 使用中文进行协作沟通
3. 保持代码风格与现有代码一致
4. 所有公开 API 必须有文档注释

## Agent 使用规则

1. 默认使用 `orchestrator` 作为入口 Agent
2. 复杂任务必须先调用 `task-planning` skill 制定计划
3. 代码变更必须经由 `reviewer` 审查
4. 测试覆盖率不得低于 80%

## 协作规范

1. Agent 之间通过 `@agent_name` 进行任务转交
2. 关键上下文信息必须在转交时传递
3. 每个 Agent 完成工作后输出明确的完成报告
4. 遇到无法解决的问题及时升级给 orchestrator