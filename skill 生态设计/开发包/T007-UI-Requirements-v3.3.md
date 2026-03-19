# T007 UI Requirements v3.3（行业版+风险治理强化）

## 0. 文档信息
- 来源基线：商业方案 v3.3
- 文档类型：UI 需求
- 版本：v3.3
- 日期：2026-03-19

## Summary
在 v3.2 UI 基础上，新增治理可视化与 L1 失败兜底体验。

## Changelog（相对 v3.2 UI）
- 新增 Learning Gate 可视化状态
- 新增担保退坡层级展示
- 新增 L1 失败兜底中心（转派/返券/ETA）

---

## 1. 页面范围
1. `/skillhub`
2. `/square/bounty/:id`
3. `/square/workbench/:id`
4. `/square/settlement/:id`
5. `/square/learning/:id`
6. `/assist/fallback/:id`
7. `/governance/gate/:caseId`

## 2. 关键页面需求
### 2.1 Learning Gate 页面
- 显示成功率、效果提升、负反馈三项阈值
- 显示 Gate 结论：Pass / Reject / Gray
- Reject 必须展示原因码

### 2.2 结算页
- 展示 NetContribution 计算明细
- 展示 T+7 倒计时与可发放状态
- 争议/回滚扣减明细可追踪

### 2.3 小白兜底页
- 自动转派状态
- 返券文案与额度
- ETA 与超时升级状态

## 3. 交互规则
- Gate 不通过：禁用“发布正式版本”按钮
- 争议中：禁用“发放分润”按钮
- ETA 超时：自动切换“官方托底处理中”

## 4. UI 验收标准
- 15 分钟可演示：交易 + 学习 + 兜底全链路
- 关键状态一致性：前后端状态无冲突
- L1 用户能看懂“失败后平台在做什么”
