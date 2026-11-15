---
tags:
  - 平台组件
  - monitoring
  - prometheus
created: 2026-11-14
---

# 📈 KPS

> kube-prometheus-stack：K8s 集群级监控的标准 Helm 全家桶——Prometheus Operator + Prometheus + Alertmanager + Grafana + node-exporter + kube-state-metrics。

## 定位

- 私有化客户集群监控的基础设施默认选型：一条 `helm install` 拉起完整监控栈
- 核心价值是 **Prometheus Operator 的 CRD 体系**：用声明式方式管理监控配置（这正是它能被 FluxCD/GitOps 管理的原因）
- 与 SigNoz 分工：KPS 管集群级（节点/Pod/控制面指标 + 经典告警），SigNoz 管应用级（trace/APM/日志）

## 核心主题（合并为一篇实战向大笔记）

- [[Prometheus Operator CRD]] — ServiceMonitor / PodMonitor / PrometheusRule / AlertmanagerConfig：声明式监控配置的核心
- [[KPS 组件清单]] — 各组件职责与默认部署（Prometheus/Alertmanager/Grafana/exporters）
- [[helm 部署与定制]] — values 定制、资源规格、存储（持久化 Prometheus 数据）、Fleet 场景的统一配置
- [[内置告警规则]] — kubernetes-mixin 默认规则、哪些该开、告警对接（→ [[Keep]]）
- [[Grafana 与看板]] — 内置 dashboard、多集群看板组织
- [[多集群监控架构]] — 每集群 KPS + remote write 汇聚（与 [[多集群观测方案]] 呼应）
- [[数据保留与容量]] — retention、存储估算、 downsampling 缺失问题（→ Thanos/Mimir 选型）

## 与平台的关系

- 每个客户集群的标准监控栈；指标经 remote write 代理回云平台 → [[02-可观测性]]
- 由 [[FluxCD]] HelmRelease 交付

## 相关

- 上游：[[平台组件]] · [[云原生]]
- 兄弟：[[SigNoz]]（应用级）· [[Keep]]（告警聚合）
