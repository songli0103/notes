---
tags:
  - kapp
  - 流程
  - 待深化
created: 2026-11-16
---

# K8s 安装流程（整体 A，骨架待深化）

> 整体 A：从无到有装 K8s。已知 carrier：[[kurl-fork]]（安装引擎，kURL fork：addons/bundles/packages）、[[k8s-setup]]（amd64/arm64 离线包、images.json、push.sh、scripts）。
> 交接出口 → [[集群接入与agent安装]]。

## 已知事实

- kurl-fork 保留 kURL 结构：`addons/`（24 目录）、`bundles/`、`packages/`、`cmd/kurl`、`scripts/`。
- k8s-setup 按架构分目录（amd64/arm64 k8s 包），`images.json` 镜像清单 + `push.sh` 推送。
- kapp 安装模板里 `kapp-cli cluster install … --agent-deploy-cmd` 与整体 A 入口同源（见 [[集群接入与agent安装]]）。

## 待调研

- [ ] kurl-fork 相对上游 kURL 的 fork 改动点（离线化？定制 addon？）
- [ ] k8s-setup 产物如何被 kurl/kapp-cli 消费（OBS？OCI？）
- [ ] 安装脚本链：installk8s 模板 → kapp-cli → kurl 的调用关系
- [ ] 与 [[集群接入与agent安装]] 的精确交接（kubeconfig/注册时机）

## 关联

- [[kapp平台总览]]、[[kurl-fork]]、[[k8s-setup]]