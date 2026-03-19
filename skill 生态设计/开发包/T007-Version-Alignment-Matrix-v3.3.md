# T007 Version Alignment Matrix v3.3

## 0. 文档信息
- 版本：v3.3
- 日期：2026-03-19
- 目的：确保商业化方案、PRD、UI、TRD 在范围、规则、字段与验收口径上一致

## Summary
- 3.3 已完成商业方案 + PRD + UI + TRD 同版本对齐
- 本矩阵用于开发前冻结口径，减少跨文档歧义

## Changelog
- 新增 v3.3 对齐矩阵

---

## 1. 文档对齐总表
| 维度 | 商业化方案 v3.3 | PRD v3.3 | UI v3.3 | TRD v3.3 | 对齐状态 |
|---|---|---|---|---|---|
| 主叙事双引擎 | Agent Square + Skill Loop | ✅ | ✅ | ✅ | ✅ |
| Learning Gate 强制前置 | 第18章 | 第4章 | Gate页面/交互约束 | Gate硬校验 | ✅ |
| 净贡献值 + T+7 | 第19章 | 第4章/第5章 | 结算明细页 | 结算服务与字段 | ✅ |
| 担保退坡双指标 | 第20章 | 第4章 | 分层状态展示 | S1/S2/S3流转规则 | ✅ |
| Fail-to-Learn 标准化 | 第21章 | 第4章/第5章 | 学习看板/兜底页 | fallback+learning case | ✅ |
| L1失败兜底三件套 | 第21.4节 | 第5.3节 | fallback页面 | fallback服务接口 | ✅ |

---

## 2. 字段级对齐（关键）
| 业务概念 | PRD 字段语义 | UI 展示字段 | TRD 存储/接口 |
|---|---|---|---|
| Learning Gate 结果 | gate_status | learning_gate.status | learning_gate_results.status |
| 净贡献值 | net_contribution | settlement.net_contribution | learning_contributions.net_contribution |
| T+7 可发放时间 | payout_available_at | settlement.available_at | settlement_payouts.available_at |
| 兜底状态 | fallback_status | fallback.ticket_status | fallback_tickets.status |
| ETA | fallback_eta | fallback.eta | fallback_tickets.eta_at |

---

## 3. 冻结口径（开发前）
1. Learning Gate 未通过，不允许正式版本发布。
2. 分润一律走 T+7 可发放窗口。
3. ETA 超时自动升级官方托底，不可人工跳过。
4. 所有治理动作必须有审计日志。

---

## 4. 风险项与处理
| 风险 | 影响 | 处理措施 |
|---|---|---|
| 文档口径漂移 | 开发返工 | 以本矩阵为唯一对齐基准 |
| 阈值争议 | 评审卡住 | 先按 v3.3 拍板阈值执行，后续版本迭代 |
| 兜底流程不闭环 | L1流失 | 强制 ETA + 超时升级 |

---

## 5. 结论
v3.3 的业务规则、产品需求、界面表达、技术实现已完成可开发级对齐。