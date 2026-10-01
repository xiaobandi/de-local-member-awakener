# 储值流失预警

> 余额高但 60 天未到店 → 红色预警+挽留方案

工作流 `wf-local-member-storedvalue-churn`　·　归属 会员唤醒师　·　触发 定时（每周）　·　
复杂度 S　·　阶段 P1

## 调用链

- `RFM 分层`（rfm-segmentation）

## 文档

- [`WORKFLOW.md`](WORKFLOW.md) — 完整编排、闸门、降级与验收标准
- [`tests/cases.yaml`](tests/cases.yaml) — 端到端 / 闸门 / 降级用例

## 一句话试用

```text
帮我跑 会员唤醒师 的「储值流失预警」：<你的输入>
```
