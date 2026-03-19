# T007 TRD v3.3（开发就绪版）

## 0. 文档信息
- 基线：PRD v3.3 / 商业方案 v3.3
- 版本：v3.3
- 日期：2026-03-19
- 状态：Ready for Dev

## Summary
本版 TRD 对齐 v3.3 全量规则，明确服务拆分、数据结构、接口契约、任务调度与验收标准。

## Changelog（相对旧版 v3.3 TRD）
- 增补状态机、表结构、时序任务、错误码、监控指标

---

## 1. 技术架构
- Frontend：SvelteKit
- API：NestJS
- DB：PostgreSQL
- Queue/Cache：Redis
- Audit：Append-only Log + 事件流

服务域：
1. Square Service（任务/提案/交付）
2. Learning Service（learning case / Gate / patch）
3. Settlement Service（净贡献/分润）
4. Governance Service（担保退坡/争议）
5. Fallback Service（L1兜底）

---

## 2. 状态机
### 2.1 任务状态
draft -> open -> submitted -> awarded -> delivered -> settled
异常：delivered -> disputed -> settled

### 2.2 分润状态
pending -> hold -> releasable -> released
异常：任意 -> clawback

### 2.3 兜底状态
created -> dispatched -> refunded -> resolved
异常：超时 -> escalated

---

## 3. 数据模型（核心）
- `tasks`：基础任务
- `task_proposals`：提案
- `task_deliveries`：交付物
- `learning_cases`：失败/边界问题案例
- `learning_gate_results`：阈值计算与结论
- `skill_patches`：灰度/正式补丁
- `learning_contributions`：贡献与净贡献字段
- `settlement_payouts`：分润记录与可发放时间
- `fallback_tickets`：兜底流程与 ETA
- `audit_events`：关键治理审计

关键字段：
- `learning_gate_results`: success_rate, impact_gain, negative_feedback, status, reason_code
- `settlement_payouts`: net_contribution, payout_status, available_at, released_at
- `fallback_tickets`: status, eta_at, escalated_at, refund_ratio

---

## 4. API 契约（核心）
- `POST /learning/cases`
- `POST /learning/cases/{id}/gate-evaluate`
- `POST /skills/{id}/patches/{patchId}/promote`
- `POST /settlement/{taskId}/calc-net-contribution`
- `POST /settlement/{taskId}/schedule-payout`
- `POST /fallback/{taskId}/auto-dispatch`
- `POST /fallback/{taskId}/refund`
- `POST /fallback/{taskId}/escalate`

错误码建议：
- `GATE_NOT_PASS`
- `PAYOUT_NOT_RELEASABLE`
- `FALLBACK_NOT_TIMEOUT`
- `INVALID_STATUS_TRANSITION`

---

## 5. 规则执行
### 5.1 Gate 规则
Pass 条件：
- success_rate >= 0.80
- impact_gain >= 0.15
- negative_feedback <= 0.10
否则 Reject，附 reason_code。

### 5.2 分润规则
`NetContribution = PositiveImpact - RollbackLoss - DisputePenalty`
- 创建后进入 pending
- T+7 到期切 releasable
- 审核通过 released

### 5.3 兜底规则
- 任务失败自动建 fallback_ticket
- 自动发返券
- 生成 ETA
- ETA 超时自动 escalate

---

## 6. 调度与任务
- Cron-1：每小时扫描 payout available_at 到期任务
- Cron-2：每15分钟扫描 fallback ETA 超时任务
- Cron-3：每日对账任务（分润/返券一致性）

---

## 7. 可观测性
指标：
- Gate pass/reject 比例
- payout 状态分布
- fallback 超时率
- 状态机非法迁移次数

告警：
- Gate 服务错误率 > 2%
- 分润延迟任务 > 阈值
- 超时未升级兜底任务 > 0

---

## 8. 测试与验收
- 单测：规则计算与状态机迁移
- 集成：成交->学习->分润->兜底全链路
- 回归：账务一致性 100%
- 验收：关键流程 0 阻塞缺陷
