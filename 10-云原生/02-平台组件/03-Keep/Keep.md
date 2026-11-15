---
tags:
  - 平台组件
  - alerting
  - workflow
created: 2026-11-14
---

# 🔔 Keep

> 开源告警管理与响应平台（keephq/keep）：把各处告警（Alertmanager、Prometheus、SigNoz……）汇到一处，做去重、聚合、工作流自动化。

## 定位

- 解决「告警风暴」问题：多来源告警 → 去重 → 分组聚合 → 关联 → 路由
- 内置 Provider 体系：Alertmanager、Prometheus、Grafana、K8s 事件、Webhook 等几十种告警源接入
- **Workflow 引擎**：YAML/Python 定义告警处理工作流（自动诊断、通知、扩容动作）——是 AIOps 的天然切入点
- 有 AI 能力（告警摘要/关联分析），与平台 AIOps 助手方向契合

## 核心主题（合并为一篇实战向大笔记）

- [[告警风暴与治理]] — 去重/聚合/抑制/静默的分层思路；为什么 Alertmanager 不够用
- [[Provider 接入]] — 告警源接入模型（polling/webhook）、Alertmanager 对接
- [[告警工作流]] — Keep Workflow 语法、触发器、动作节点、定时巡检
- [[告警生命周期]] — firing→resolved、关联事件、值班与通知策略
- [[AI 与告警]] — 内置 AI 摘要/关联；与自建 AIOps 助手的集成点
- [[部署与 HA]] — K8s 部署、数据库依赖、私有化离线安装

## 与平台的关系

- 云平台的统一告警面板：各客户集群 Alertmanager/KPS 告警汇聚到平台侧 Keep
- Workflow 引擎与 [[Pi-agent]] 互补：Keep 做告警侧自动化，Pi-agent 做诊断侧交互

## 相关

- 上游：[[平台组件]] · [[云原生]]
- 兄弟：[[KPS]]（告警源）· [[SigNoz]]（告警源）
