---
tags:
  - kapp
  - pevent
  - 组件
created: 2026-11-16
---

# pevent（组件卡）

> 定位：kapp 仓库内的**一次性 Job 二进制**（`cmd/pevent`），客户集群里干部署重活的工人；与 [[kapp-agent]] 零直连，靠 K8s Job 物化、靠 Connect 直报云。
> 参与流程：[[组件部署流程]]。横切 → [[双通道通信架构]]、[[Proto契约与代码生成]]、[[令牌与信封加密]]。入口 → [[kapp平台总览]]。

## 1. 形态

- 子命令：`deploy / apply / patch`（`cmd/pevent/root.go`）；由 agent `Jobs.Create` 拉起，镜像默认 kapp 镜像。
- 必填 flag：`--event-id / --apiserver / --token / --secret-key`（+`--timeout`），来自 JobSpec.Args（参数流）。
- 与 apiserver **同仓共享** `api/gen` 与客户端封装 `internal/apps/apiserver/client`（Clientset+Bearer），一次生成两边用。

## 2. 上行 RPC（边干边报）

| 方法 | 时机 | 锚点 |
|---|---|---|
| Event.AcceptOpsEvent | 启动领事件（5s/5 次重试，AES 解密；无 key 兼容老 agent 明文） | `process/cloudevent_process.go` L47/L99 |
| Event.NotifyOpsEvent | 结果通知（重试） | 同上 L189 |
| DeployTaskComponent.SetComponentStatus / SetComponentDetail / SetCompDeployStage | 部署进度 | `deploy/process.go` L284/L402/L433 |
| DeployTaskComponent.GetExtraYaml | 取附加配置 | `remote/mysql.go` L24 |
| ComponentLifecycle.ResolveLifecycleProvider | 生命周期钩子 | `lifecycle/apiserver_provider.go` L21 |

## 3. 执行与观测

- 执行：helm/flux 写 CR（声明式下发），loop 刷新更新时间（`loop.go` L125）。
- 观测：Pod 日志被 agent `GetLogs` 转远程日志——pevent 自己不持有观测通道。
- 生命周期：Job backoffLimit2/TTL1d 由 agent 侧 jobrun 设定。

## 4. 关联

- [[kapp-agent]]、[[apiserver]]、[[组件部署流程]]、[[kapp平台总览]]