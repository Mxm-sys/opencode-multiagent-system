# 项目规则

## 决策层规则

1. 默认入口 Agent 为 `presider`
2. 三个 Architect（alpha/beta/gamma）使用**完全相同的提示词**，仅 agent key 不同
3. Architect 之间互不通信，各自独立产出方案
4. 所有 Architect 方案必须按 JSON 格式输出
5. Judge 裁决必须明确，不允许"并列"
6. 安全性一票否决：高危风险且无应对 → 直接淘汰

## 协作规范

1. Agent 之间通过 `@agent_name` 进行任务转交
2. Presider 转交需求时必须传递完整上下文
3. 方案 JSON 必须包含全部字段，不能省略
4. 使用中文进行协作沟通