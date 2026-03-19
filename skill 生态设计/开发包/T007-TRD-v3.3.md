# T007 TRD v3.3（行业版+风险治理强化）

## 0. 文档信息
- 来源基线：商业方案 v3.3
- 文档类型：TRD
- 版本：v3.3
- 日期：2026-03-19

## Summary
在 v3.2 技术基线下，补齐治理与兜底机制的可执行实现。

## Changelog（相对 v3.2 TRD）
- 强化 Learning Gate 为硬校验流程
- 新增 NetContribution + T+7 分润流程实现细节
- 新增 fallback 托底超时升级机制

---

## 1. 架构与服务
- Frontend: SvelteKit
- API: NestJS
- DB: PostgreSQL
- Cache/Queue: Redis
- AuditLog: append-only

服务：
1) Square Service
2) Settlement Service
3) Learning Service
4) Governance Service
5) Fallback Service

## 2. 数据模型（新增/强化）
- `learning_gate_results`（新增阈值字段 + reason_code）
- `learning_contributions`（net_contribution 计算字段）
- `settlement_payouts`（available_at = created_at + 7d）
- `fallback_tickets`（eta_at, escalated_at, escalation_reason）

## 3. 核心接口
- `POST /learning/cases/{id}/gate-evaluate`
- `POST /skills/{id}/patches/{patchId}/promote`（仅 Gate Pass）
- `POST /settlement/{taskId}/calc-net-contribution`
- `POST /settlement/{taskId}/schedule-payout`
- `POST /fallback/{taskId}/auto-dispatch`
- `POST /fallback/{taskId}/escalate`

## 4. 规则实现
### 4.1 Learning Gate（强制）
- success_rate >= 0.80
- impact_gain >= 0.15
- negative_feedback <= 0.10
- 任一不满足 => Reject

### 4.2 分润
`NetContribution = PositiveImpact - RollbackLoss - DisputePenalty`
- payout_available_at = now + 7 days

### 4.3 担保退坡
- 指标：completed_orders 与 dispute_rate
- 状态：S1/S2/S3 自动流转

### 4.4 L1 兜底
- 失败触发 fallback_ticket
- 推送返券文案
- 生成 ETA
- 超时自动 escalate 到官方托底

## 5. 技术验收
- Gate 判定可重复且可审计
- T+7 结算时间准确
- fallback 超时升级触发准确率 >= 99%
- 账务一致性（分润/返券）100%
