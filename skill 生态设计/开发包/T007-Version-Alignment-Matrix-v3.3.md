# T007 Version Alignment Matrix v3.3（开发就绪版）

## 0. 文档信息
- 版本：v3.3
- 日期：2026-03-19
- 目的：统一商业方案、PRD、UI、TRD、Kickoff 的开发口径。

## Summary
- 本矩阵作为 v3.3 单一对齐基准（Single Source of Alignment）。

## Changelog
- 升级为开发就绪矩阵：增加章节映射、字段映射、验收映射、责任人映射。

---

## 1. 章节映射
| 能力域 | 商业化方案 v3.3 | PRD v3.3 | UI v3.3 | TRD v3.3 | 状态 |
|---|---|---|---|---|---|
| 成交闭环 | 3/5/10/11 | 3/5/6 | 2.1/2.3 | 2.1/3/4 | ✅ |
| 学习闭环 | 4/18/21 | 3/5/6 | 2.2/2.4 | 2.2/5 | ✅ |
| Gate 强制前置 | 18/22 | 5/6 | 2.2/4 | 5.1 | ✅ |
| 分润机制 | 19/22 | 5/6 | 2.3/3 | 2.2/5.2 | ✅ |
| 担保退坡 | 20/22 | 5 | 2.1 | 5.3 | ✅ |
| L1兜底 | 21.4/22 | 5/6 | 2.4/5 | 2.3/5.3 | ✅ |

---

## 2. 字段对齐
| 业务字段 | PRD 定义 | UI 字段 | TRD 字段/表 | 验收检查 |
|---|---|---|---|---|
| gate_status | FR-05 | learning_gate.status | learning_gate_results.status | Gate 不可绕过 |
| net_contribution | FR-07 | settlement.net_contribution | learning_contributions.net_contribution | 对账一致 |
| payout_status | FR-08 | settlement.payout_status | settlement_payouts.payout_status | T+7 生效 |
| available_at | FR-08 | settlement.available_at | settlement_payouts.available_at | 到期可发放 |
| fallback_status | FR-09 | fallback.ticket_status | fallback_tickets.status | 超时升级 |
| eta_at | FR-09 | fallback.eta | fallback_tickets.eta_at | ETA 准确 |

---

## 3. 验收对齐
| 验收项 | PRD | UI | TRD | Kickoff | 状态 |
|---|---|---|---|---|---|
| 成交闭环可演示 | ✅ | ✅ | ✅ | ✅ | ✅ |
| Gate 强制有效 | ✅ | ✅ | ✅ | ✅ | ✅ |
| T+7 分润有效 | ✅ | ✅ | ✅ | ✅ | ✅ |
| 兜底闭环有效 | ✅ | ✅ | ✅ | ✅ | ✅ |
| 审计追踪完整 | ✅ | - | ✅ | ✅ | ✅ |

---

## 4. 责任人对齐
| 模块 | PM | UI/UX | Tech Lead | QA | Ops |
|---|---|---|---|---|---|
| Gate | A | C | R | R | C |
| Settlement | A | C | R | R | C |
| Fallback | A | R | R | R | R |
| 审计与告警 | C | - | R | C | R |

> 说明：R=负责，A=拍板，C=协作

---

## 5. 冻结口径
1. 未通过 Gate 不得发布正式补丁。
2. 分润必须经过 T+7 才可 released。
3. 兜底 ETA 超时必须 escalated。
4. 所有关键动作必须写入审计日志。

---

## 6. 结论
v3.3 文档链路已完成“可开发、可测试、可上线”一致性对齐。