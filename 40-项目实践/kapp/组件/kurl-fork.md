---
tags:
  - kapp
  - kurl
  - 组件
  - 待深化
created: 2026-11-16
---

# kurl-fork（组件卡，待深化）

> 定位：整体 A 的 **K8s 安装引擎**，kURL 的 fork（addons/bundles/packages 结构保留）。
> 流程 → [[K8s安装流程]]。入口 → [[kapp平台总览]]。

## 已知事实

- 结构同上游 kURL：`addons/`（24 目录）、`bundles/`、`packages/`、`cmd/kurl`、`kurl_util/`、`scripts/`、`testgrid/specs`。
- 有 `ARCHITECTURE.md`、`design/` 可读。

## 待调研

- [ ] fork 改动点：离线化？定制 addon（registry/rook/longhorn?）？arm64 支持？
- [ ] 与 k8s-setup 产物的消费关系
- [ ] kapp-cli cluster install 如何调起 kurl

## 关联

- [[kapp平台总览]]、[[K8s安装流程]]、[[k8s-setup]]、[[集群接入与agent安装]]