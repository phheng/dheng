# T007 UI Requirements v3.3（开发就绪版）

## 0. 文档信息
- 基线：PRD v3.3 / 商业方案 v3.3
- 版本：v3.3
- 日期：2026-03-19
- 状态：Ready for Dev

## Summary
- UI 目标：让“成交、学习、治理、兜底”四条链路在前端可见、可理解、可追踪。

## Changelog（相对旧版 v3.3 UI）
- 增补页面级字段、状态、交互限制、异常态与文案策略

---

## 1. 页面清单
1. SkillHub 首页 `/skillhub`
2. 任务详情 `/square/bounty/:id`
3. 工作台 `/square/workbench/:id`
4. 结算页 `/square/settlement/:id`
5. 学习看板 `/square/learning/:id`
6. 兜底中心 `/assist/fallback/:id`
7. Gate 评估页 `/governance/gate/:caseId`

---

## 2. 页面需求细化
## 2.1 任务详情页
- 信息区：预算、截止时间、验收标准、担保等级
- 状态区：状态时间轴（open->awarded->delivered->settled）
- 操作区：提案、中标、交付、争议入口

## 2.2 Gate 评估页
- 指标卡：success_rate / impact_gain / negative_feedback
- 结果标签：PASS / REJECT
- REJECT 时展示 reason_code + 建议动作
- 按钮约束：Pass 前“发布正式版本”禁用

## 2.3 结算页
- 账务区：平台抽佣、净贡献值、应发分润
- 时间区：T+7 倒计时
- 风险区：争议扣减、回滚扣减明细

## 2.4 兜底中心
- 流程条：自动转派 -> 返券 -> ETA -> 托底结果
- 返券卡：返券比例、到账时间、说明文案
- ETA 卡：预计修复时间、超时自动升级提示

---

## 3. 状态设计
- TaskStatus: draft/open/submitted/awarded/delivered/settled/disputed
- GateStatus: pending/pass/reject
- PayoutStatus: pending/hold/releasable/released/clawback
- FallbackStatus: created/dispatched/refunded/resolved/escalated

---

## 4. 交互约束
1. 未中标禁止提交交付。
2. Gate 未通过禁止正式发布。
3. 争议中禁止分润发放。
4. ETA 超时自动切换 escalated，不允许手动忽略。

---

## 5. 文案策略（L1 优先）
- 成功：明确结果与下一步。
- 失败修复中：告知“已自动修复中”。
- 补偿：明确返券比例和到账时间。
- 超时：明确“已升级官方托底”。

---

## 6. 可用性要求
- 关键状态 2 跳内可见
- 首屏显示“当前处于哪个流程阶段”
- 错误提示具备可执行下一步

---

## 7. UI 验收
- 15 分钟演示四链路完整打通
- 状态与后端一致（抽检 20 条）
- L1 用户可理解失败后的处理进度
