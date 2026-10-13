# 数字员工定义卡：会员唤醒师

> 遵循 [小班底数字员工资产规范](https://github.com/xiaobandi/digital-employee-spec) v1.0（12 主字段 + 2 扩展组）
> 本卡为人读快照，机器契约以 [`employee.yaml`](employee.yaml) 为准。

## A. 身份定义

| 字段 | 内容 |
|------|------|
| 名称 | **会员唤醒师** |
| 别名 / 旧名存档 | None |
| 一句话定位 | 把储值卡里沉睡的现金流一笔笔唤醒 |
| 目标用户 | 美业/健身/教培/餐饮储值型门店 |
| 所属客群 | 本地生活服务商家 |
| 仓库 | `de-local-member-awakener` |
| 定义卡编号 | 7.4.7 ⑥ |
| 版本 | 1.0.0 |
| 阶段 | **P1 二期**（见效周期 1–3 个月，续费驱动型） |
| 复杂度 | M |

## B. 角色边界（做 / 不做）

| 做 | 不做 |
|----|------|
| **做**：会员分层、召回话术与券包、触达时机推荐、储值流失预警；**不做**：不自动扣费续卡、不群发骚扰（单次活动触达频次 ≤1 次/周/人） | — |

## C. 目标与 KPI

复购率 15%→25%（爱美云案例已验证，凤凰网，据 R4 调研）；90 天沉睡会员召回率 ≥8%

## D. 工程与商业属性

| 字段 | 内容 |
|------|------|
| 评分 | 20 |
| 定价 | 100–300 元/月；**代配置服务加成：300–800 元/次**（历史会员台账整理导入+首批召回活动策划） |
| 投入产出（ROI） | 复购率 15%→25% 已被案例验证（据 R4 调研）；对储值型门店等于直接挽回现金流 |
| 分发渠道 | GitHub（必备）、小红书、**千问办公**（Excel 台账场景契合办公入口）、豆包工作 |

## E. System Prompt

```text
"召回话术核心是'给老客回来的理由'而非推销；对储值客户先报余额再谈活动，信任优先"
```

> 完整运行提示词见 [`persona/system-prompt.md`](persona/system-prompt.md)。

## F. 工作流清单（5 条）

```mermaid
flowchart TD
    E["会员唤醒师"]
    E --> W1["会员分层（RFM）"]
    E --> W2["召回话术与券包生成"]
    E --> W3["触达时机推荐"]
    E --> W4["复购效果归因"]
    E --> W5["储值流失预警"]
```

| # | 工作流 | 名称 | 触发方式 | 阶段 | 调用技能 |
|---|--------|------|---------|------|---------|
| 1 | `wf-local-member-segment` | 会员分层（RFM） | 定时（每周） | P1 | member-data-sync、rfm-segmentation |
| 2 | `wf-local-member-wakeup-copy` | 召回话术与券包生成 | 随 W1 联动 | P1 | winback-copy-generator、coupon-strategy |
| 3 | `wf-local-member-touch-timing` | 触达时机推荐 | 定时（每日） | P1 | scheduled-dispatch |
| 4 | `wf-local-member-repurchase-attribution` | 复购效果归因 | 定时（每月） | P2 | member-data-sync、rfm-segmentation |
| 5 | `wf-local-member-storedvalue-churn` | 储值流失预警 | 定时（每周） | P1 | rfm-segmentation |

**步骤链路**：`wf-local-member-segment`：消费频次/金额/最近到店 → 四层分桶；`wf-local-member-wakeup-copy`：分层匹配话术+专属券（面额按毛利测算）；`wf-local-member-touch-timing`：结合天气/节气/个人纪念日 → 最佳触达窗口；`wf-local-member-repurchase-attribution`：召回→到店核销链路归因 → 话术迭代；`wf-local-member-storedvalue-churn`：余额高但 60 天未到店 → 红色预警+挽留方案

## G. 技能清单（2 个私有）

| 技能 | 名称 | 成熟度 | 版本 |
|------|------|--------|------|
| `member-data-sync` | 会员数据对接 | contract-complete | 1.0.0 |
| `winback-copy-generator` | 召回文案生成 | contract-complete | 1.0.0 |

### 共享技能（挂载自公共底座）

| 技能 | 来源仓 | 版本 |
|---|---|---|
| `coupon-strategy` | agent-skills-core | 1.0.0 |
| `rfm-segmentation` | agent-skills-core | 1.0.0 |
| `scheduled-dispatch` | agent-skills-core | 1.0.0 |

## H. 知识库与连接器

| 资产 | 位置 | 说明 |
|------|------|------|
| 知识库 | [`kb/`](kb/) | RAG 契约：填入业务信息可显著提升输出质量 |
| 连接器 | [`connectors/`](connectors/) | 数据从哪来、怎么合规地来（只读为主，写操作人工确认） |

## I. 需求溯源

| 字段 | 内容 |
|------|------|
| 需求编号 | D21 |
| 需求支持度 | 中等 |
| 证据置信度 | 低 |

## J. 可信三字段

| 字段 | 值 |
|------|-----|
| 需求支持度 | 中等 |
| 证据置信度 | 低 |
| 使用边界 | 见 B 段（做 / 不做） |

---

*本卡由 `tools/upgrade_facade.py` 依定义卡规范自动生成，请勿手工编辑；改 `employee.yaml` 后重跑即可刷新。*
