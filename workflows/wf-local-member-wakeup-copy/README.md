# 召回话术与券包生成

> 分层匹配话术+专属券（面额按毛利测算）

工作流 `wf-local-member-wakeup-copy`　·　归属 会员唤醒师　·　触发 随 W1 联动　·　
复杂度 S　·　阶段 P1

## 调用链

- `召回文案生成`（winback-copy-generator）
- `优惠券策略`（coupon-strategy）

## 文档

- [`WORKFLOW.md`](WORKFLOW.md) — 完整编排、闸门、降级与验收标准
- [`tests/cases.yaml`](tests/cases.yaml) — 端到端 / 闸门 / 降级用例

## 一句话试用

```text
帮我跑 会员唤醒师 的「召回话术与券包生成」：<你的输入>
```
