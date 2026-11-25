---
tags:
  - kapp
  - tfjob
  - 组件
  - 待深化
created: 2026-11-16
---

# kapp-tfjob（组件卡，待深化）

> 定位：整体 B 中**云资源 provisioning** 的 Terraform Job 镜像（aliyun/huaweicloud 模块 + tofu 1.9.0 + terragrunt）。
> 入口 → [[kapp平台总览]]。

## 已知事实

- 目录：`aliyun/`、`huaweicloud/`（多云 terraform 模块）、`go/`（辅助代码）、Dockerfile。
- 携带 `tofu_1.9.0_linux_amd64.tar.gz`、`terragrunt_linux_amd64`、`terraform-plugin-dir.tar.gz`、`kapp-cli`。

## 待调研

- [ ] kapp 哪个服务/事件触发 tfjob（worker？deploy_task？Job 形态同 pevent？）
- [ ] state 存哪（OBS？后端？）、凭证注入方式
- [ ] 与 [[组件部署流程]] 的关系（先 provision 云资源再部署组件？）

## 关联

- [[kapp平台总览]]、[[apiserver]]、[[pevent]]