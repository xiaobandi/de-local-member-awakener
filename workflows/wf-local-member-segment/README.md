# 会员分层（RFM）

> 消费频次/金额/最近到店 → 四层分桶

工作流 `wf-local-member-segment`　·　归属 会员唤醒师　·　触发 定时（每周）　·　
复杂度 M　·　阶段 P1

## 调用链

- `会员数据对接`（member-data-sync）
- `RFM 分层`（rfm-segmentation）

## 文档

- [`WORKFLOW.md`](WORKFLOW.md) — 完整编排、闸门、降级与验收标准
- [`tests/cases.yaml`](tests/cases.yaml) — 端到端 / 闸门 / 降级用例

## 一句话试用

```text
帮我跑 会员唤醒师 的「会员分层（RFM）」：<你的输入>
```
