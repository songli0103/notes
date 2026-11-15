---
tags:
  - 平台组件
  - observability
  - apm
created: 2026-11-14
---

# 🔍 SigNoz

> 开源一体化观测平台（APM）：Metrics + Traces + Logs 基于 OpenTelemetry 原生整合，ClickHouse 存储——客户集群应用级观测的候选后端。

## 定位

- 一站式：应用指标（RED）、分布式追踪、日志查询、关联分析，一个平台全包
- OpenTelemetry 原生：数据采集端用 OTel Collector，不锁定厂商
- ClickHouse 做存储引擎：大数据量下的查询性能是卖点
- 与「监控栈」（KPS）的分工：KPS 管集群级监控（节点/Pod/告警），SigNoz 管应用级观测（trace/APM/日志）

## 核心主题（合并为一篇实战向大笔记）

- [[SigNoz 架构]] — otel-collector（数据接入）+ query-service + ClickHouse + frontend 各组件职责
- [[OpenTelemetry 接入]] — OTel SDK/Collector 配置、自动探针（Go 应用接入）、span/trace 模型
- [[ClickHouse 存储模型]] — 表结构、保留策略（retention）、磁盘占用与查询性能
- [[Trace 与 Metrics 关联]] — SpanMetrics、服务拓扑图、RED 指标从 trace 生成
- [[SigNoz 告警]] — 基于指标/trace 的告警规则、与 Alertmanager/Keep 的对接
- [[选型对比]] — SigNoz vs Jaeger+Prometheus+Loki 组合 vs Grafana 栈 vs 商业 APM
- [[私有化考量]] — 离线部署、资源规格、多客户数据隔离（租户模型）

## 与平台的关系

- 客户集群的应用观测后端候选；与 [[02-可观测性]]（方法论与多集群架构）互为具体实现
- 应用层接入 Go 服务 → [[Go 开发]]

## 相关

- 上游：[[平台组件]] · [[云原生]]
- 兄弟：[[KPS]]（集群级监控）· [[Keep]]（告警聚合）
