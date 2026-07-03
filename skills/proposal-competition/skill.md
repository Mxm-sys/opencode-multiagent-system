# 三学士献计 Skill — 方案竞优

将同一需求分派给三个独立的 Architect 实例并行产出方案，再由 Judge 裁决选出最优方案。

## 适用场景

- 架构设计决策（选缓存方案、选异步策略、选数据结构等）
- 复杂 Bug 修复方案（可能有多种修法）
- 重构方案选择（有多种重构路径）
- 任何"一题多解"且需要择优的技术决策

## 不适用场景

- 简单的文案修改、配置调整（直接做即可，不值得三倍成本）
- 紧急修复（来不及走决策流程）

## 完整流程

### 第一步：三学士献计

Presider 将同一需求分派给三个 Architect：

```
@architect_alpha  请针对以下需求给出方案：[需求]
@architect_beta   请针对以下需求给出方案：[需求]
@architect_gamma  请针对以下需求给出方案：[需求]
```

三个 Architect 使用**完全相同的提示词**，但各自独立运行，互不干扰。

每个 Architect 输出一份结构化方案 JSON：
- `proposal_alpha.json`
- `proposal_beta.json`
- `proposal_gamma.json`

方案必须包含：解决思路、改动文件列表、风险预估、预估复杂度。

### 第二步：内阁票拟（裁决）

Presider 将三份方案汇总后交给 Judge：

```
@judge 请对以下三份方案进行裁决：
- Alpha: [proposal_alpha 摘要]
- Beta:  [proposal_beta 摘要]
- Gamma: [proposal_gamma 摘要]
```

Judge 按七个维度（可行性、最小改动、安全性、风险控制、复杂度、可测试性、可维护性）打分，输出裁决书，指定胜者。

### 第三步：钦点执行

Presider 输出最终决策结果，将胜出方案移交执行层（Operator）。

Operator 只负责照方案执行，不再参与设计决策。

## 成本估算

| 阶段 | Agent 数量 | Token 消耗 |
|------|-----------|-----------|
| 献计 | 3x Architect | ~3x（设计思考） |
| 裁决 | 1x Judge | ~1x（对比分析） |
| 执行 | 1x Operator | ~1x（编码实现） |
| **合计** | | ~5x（而非 3x3=9x） |

> 关键优势：设计阶段 3 倍思考，执行阶段仍 1 倍，避免了三份代码 diff 合并的灾难。

## 调用方式

```
@presider 请使用 proposal-competition 技能处理以下需求：[需求描述]
```