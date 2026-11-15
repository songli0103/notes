---
tags:
  - 平台组件
  - certificates
  - tls
created: 2026-11-14
---

# 📜 cert-manager

> K8s 证书自动签发与轮换控制器：集群内所有 TLS 证书的自动化发证、续期、注入——私有化场景证书管理的标配。

## 定位

- 声明式证书管理：`Certificate` CRD 描述「要什么证书」，cert-manager 负责签发 + 续期 + 存 Secret
- 支持多种签发源：ACME（Let's Encrypt）、自签、内部 CA、Vault、外部私有 CA
- 私有化场景的核心价值：客户环境没有公网域名/ACME 时，用**内部 CA 链**统一管理集群证书
- 解决的痛点：手动管证书 = 过期事故；K8s 自身组件证书（kubeadm）不归它管，它管工作负载层

## 核心主题（合并为一篇实战向大笔记）

- [[cert-manager 架构]] — Controller / webhook / cainjector 三组件职责
- [[Issuer 与 ClusterIssuer]] — 签发者抽象、命名空间边界
- [[Certificate CRD]] — 证书请求建模、Secret 管理、续期窗口
- [[ACME 签发]] — HTTP-01/DNS-01 challenge、Let's Encrypt 流程
- [[内部 CA 体系]] — 自签根 CA → 中间 CA → 工作负载证书的链设计（私有化主线）
- [[Ingress 与证书注入]] — ingress-shim 自动签发、Webhook/服务间 mTLS 用法
- [[私有化证书方案]] — 离线环境证书链规划、证书监控告警、与 [[证书管理与 TLS]] 的关系

## 与平台的关系

- 平台组件的 TLS 统一管理：ingress 证书、组件间 mTLS、webhook 证书
- 由 [[FluxCD]] HelmRelease 交付

## 相关

- 上游：[[平台组件]] · [[云原生]]
- K8s 侧基础：[[06-配置与安全]]（证书管理与 TLS）
