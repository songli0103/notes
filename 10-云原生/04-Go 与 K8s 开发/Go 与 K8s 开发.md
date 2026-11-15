---
tags:
  - 云原生
  - go
  - k8s
created: 2026-11-01
updated: 2026-11-14
---

# ⚙️ Go 与 K8s 开发

> 大笔记「Go 与 K8s 开发」：用 Go 写集群内程序——从 client-go 到 Operator 到集群 agent。

## 主题清单（合并为一篇实战向大笔记）

- [[client-go 入门]] — 客户端类型、in-cluster config、RESTMapper；连 [[07-API 与 Watch 机制]]
- [[Informer 实战]] — SharedInformerFactory、事件处理、WorkQueue 用法（原理见 [[07-API 与 Watch 机制]]）
- [[controller-runtime 与 Kubebuilder]] — Operator 开发脚手架、Reconcile 实战
- [[CRD 设计实践]] — schema 定义、status/scale 子资源、多版本转换、打印列
- [[Leader Election 生产化]] — 抢 Lease、多副本 controller 高可用
- [[集群内 Agent 开发]] — DaemonSet 部署、最小权限 RBAC、证书与投影 token、资源占用控制
- [[性能与规模]] — watch 带宽、List 全量内存、分页 watch、client 限流配置

## 实战关联

- 平台 agent 的通信与架构 → [[项目实践]]
- K8s 机制原理 → [[07-API 与 Watch 机制]]（先读这篇）
- 写诊断工具 → [[Pi-agent]]（k8sgpt 模式）

## 相关

- 上游：[[云原生]] / [[Go 开发]]
