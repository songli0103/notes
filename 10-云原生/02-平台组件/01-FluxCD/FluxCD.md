---
tags:
  - 平台组件
  - gitops
  - fluxcd
created: 2026-11-14
---

# 🔄 FluxCD

> 客户集群组件交付的核心方式：GitOps Toolkit 全家桶。客户集群里跑 Flux 控制器，从 Git/OCI 源拉取期望状态并持续对账。

## 核心

- 大笔记：[[GitOps 与 FluxCD]] — 原理、v2 六控制器架构、核心 CRD、多租户、多集群 Fleet、离线源、Flux vs ArgoCD、Flagger 渐进式交付

## 组件档案

| 项 | 内容 |
|---|---|
| 官方 | fluxcd.io / github.com/fluxcd |
| 架构 | GitOps Toolkit 六控制器：source / kustomize / helm / notification / image-reflector / image-automation |
| 存储 | 无数据库（无状态控制器 + Git/OCI 为事实源）|
| 部署 | flux bootstrap，自管理（Flux 管 Flux 的 CRD）|

## 平台场景主题

- [[平台组件交付设计]] — 用 HelmRelease/Kustomization 定义平台组件栈、版本由 Git 管
- [[离线 OCI 源]] — 私有化不依赖 GitHub：镜像仓库即源（OCIRepository）、Gitea 本地 Git
- [[交付可观测]] — Flux 自身指标、notification-controller 对接事件、交付失败告警

## 相关

- 上游：[[平台组件]] · [[云原生]]
- K8s 底座：[[Kubernetes]] · Helm/Kustomize：[[09-生态与工具]]
