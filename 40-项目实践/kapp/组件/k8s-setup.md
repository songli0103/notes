---
tags:
  - kapp
  - k8s-setup
  - 组件
  - 待深化
created: 2026-11-16
---

# k8s-setup（组件卡，待深化）

> 定位：整体 A 的**离线产物仓**：按架构组织的 K8s 安装包、镜像清单与推送脚本。
> 流程 → [[K8s安装流程]]。入口 → [[kapp平台总览]]。

## 已知事实

- `amd64/k8s/`、`arm64/k8s/` 离线包目录；`scripts/`；`images.json` 镜像清单；`push.sh` 推送；README。
- 与 kapp 仓库根目录的 `images.json` 同名同构（镜像清单模式复用）。

## 待调研

- [ ] 产物形态（tar？OCI？OBS 对象？）与消费方（kurl? kapp-cli?）
- [ ] push.sh 推送目标（registry/OBS）与签名 URL 的关系（install.go OBS 4h 签名）
- [ ] 版本矩阵管理方式

## 关联

- [[kapp平台总览]]、[[K8s安装流程]]、[[kurl-fork]]、[[集群接入与agent安装]]