# T007 PRD v3.3（行业版+风险治理强化）

## 0. 文档信息
- 来源基线：商业方案 v3.3
- 文档类型：PRD
- 版本：v3.3
- 日期：2026-03-19

## Summary
1. 完整继承 v3.2 双引擎主线（成交闭环 + 学习闭环）
2. 新增治理刚性规则：Learning Gate 强制前置
3. 增加 L1 失败兜底产品化三件套（自动转派单/返券/ETA）

## Changelog（相对 v3.2 PRD）
- 新增治理规则：Learning Gate、Fail-to-Learn、担保退坡双指标
- 新增 L1 失败兜底流程与验收标准
- 对齐已拍板：净贡献值 + T+7 先执行后迭代

---

## 1. 产品目标
1) 跑通交易与学习双闭环并规模化
2) 在增长中控制质量与成本
3) 降低 L1 用户失败流失

## 2. 用户分层
- L1 小白卖家：结果导向，弱配置
- L2 运营型卖家：模板协作
- L3 高阶玩家：自建 Agent + 高阶 Skill

## 3. 核心范围（In Scope）
- Agent Square 全流程
- Skill Learning Loop（含 Learning Gate）
- 结算与分润（NetContribution + T+7）
- 担保退坡（单量+争议率）
- Fail-to-Learn 标准流程
- L1 兜底三件套

## 4. 拍板规则（强约束）
1. Learning Gate = 强制前置（未通过不得沉淀正式版本）
2. 净贡献值 + T+7 先规则化执行
3. 担保退坡按“单量+争议率”
4. Fail-to-Learn 纳入标准流程

## 5. 关键流程
### 5.1 成交流程
`draft -> open -> submitted -> awarded -> delivered -> settled`
异常：`delivered -> disputed -> settled`

### 5.2 学习流程
`failed/boundary -> collaboration -> gate-evaluate -> gray patch -> promote`

### 5.3 L1 兜底流程
`失败 -> 自动转派 -> 返券通知 -> ETA -> 超时官方托底`

## 6. 指标体系
- 北极星：周成交任务数
- 治理：Gate通过率、争议率、回滚率
- 增长：7日复购率、ARPA、抽佣收入
- 体验：L1 失败恢复成功率、平均修复时长

## 7. 验收标准
- 双闭环可完整演示
- Gate 生效且可审计
- L1 失败兜底前台可见 + 后台可追踪
- 分润/返券账务一致
