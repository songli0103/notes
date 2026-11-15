---
tags:
  - 云原生
  - gitops
  - fluxcd
created: 2026-11-01
updated: 2026-11-14
---

# 🔄 GitOps 与 FluxCD

> 大笔记「GitOps 与 FluxCD」：客户集群组件交付的核心方式——FluxCD v2 全解 + GitOps 方法论。

## 主题清单（合并为一篇面试/实战向大笔记）

- [[GitOps 原理]] — 声明式、Git 唯一事实源、pull 模式、reconciliation 与漂移纠正
- [[FluxCD v2 架构]] — GitOps Toolkit 六控制器：source / kustomize / helm / notification / image-reflector / image-automation
- [[核心 CRD]] — GitRepository / OCIRepository / Kustomization / HelmRelease / ImagePolicy
- [[Bootstrap 与自管理]] — flux bootstrap、Flux 自己管理自己的 CRD
- [[Helm 原生集成]] — helm-controller 用原生 Helm SDK：hooks / 自动回滚 / post-renderer / helm list 可见
- [[多租户]] — ServiceAccount impersonation、权限收敛
- [[多集群 Fleet]] — 每集群独立 Flux vs 集中管理；私有化场景的集群分发布局
- [[Image Automation]] — 扫描镜像仓库、ImagePolicy 选 tag、自动提交回 Git
- [[离线源]] — 不依赖 GitHub：OCI registry 源、本地 Git（Gitea）、离线 chart
- [[Flagger 渐进式交付]] — 金丝雀/A/B/蓝绿、指标门禁自动回滚
- [[Flux vs ArgoCD]] — 架构（微控制器 vs 中心化）、UI、Helm 处理、多集群模型对比
- [[CI/CD 流水线]] — push CI（构建/测试/扫描）+ pull CD（GitOps）；流水线设计
- [[发布策略]] — 滚动 / 蓝绿 / 金丝雀选型
- [[镜像构建优化]] — 多阶段构建、distroless、ko（Go 专用）

## 实战关联

- K8s 底座 → [[Kubernetes]]
- Helm/Kustomize 基础 → [[09-生态与工具]]
- 镜像仓库（Harbor/OCI 源）→ [[09-生态与工具]]

## 相关

- 上游：[[云原生]]
