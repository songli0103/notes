---
tags:
  - kapp
  - apiserver
  - 组件
created: 2026-11-16
---

# apiserver（组件卡）

> 定位：整体 B 的**云控制面**（kapp 仓库 `internal/apps/apiserver`）：业务 RPC 服务端、事件注入源、安装脚本渲染者。多服务同仓（apiserver/worker/offline/pevent/devops…）。
> 参与流程：[[组件部署流程]]、[[集群接入与agent安装]]、[[证书分发流程]]、[[集群代理查询流程]]。横切 → [[双通道通信架构]]、[[Proto契约与代码生成]]、[[令牌与信封加密]]。入口 → [[kapp平台总览]]。

## 1. 三面角色

| 面 | 动作 | 锚点 |
|---|---|---|
| 上行服务端 | Mount connect 服务端半 → handler → service → sqlc 写库（如心跳 upsert `cluster_agents`） | `api/gen/.../agentv1connect` 服务端半 |
| 下行注入 | gRPC Publish/PresenceStats（每次 Dial+Close，apikey） | `pkg/sse/grpclient.go` |
| 安装签发 | 渲染 installk8s 脚本：SubToken/ocipullToken/OBS 签名/secretInitToken + AgentDeployCmd | `services/install.go` L280-470 |

## 2. 关键服务

- Cluster：SetAgentStatus / GetMasterPasswordSalt / ReportMasterPasswordHash / ReportCertDistributeResult。
- Event：AcceptOpsEvent / NotifyOpsEvent / GetEvent（pevent 用）。
- DeployTaskComponent：SetComponentStatus/Detail/Stage、GetExtraYaml。
- AgentProxy：proxyk8s-callback 接收端（otter 缓存 request_id→chDone，2min 等待）。
- 事件组装：`services/deploy_task.go` L1854、`ops_event_notify.go` L255（`JobCommand: "pevent deploy"`）。

## 3. 同仓兄弟

- [[pevent]]：共享 client 封装与生成物。
- offline：`KappInstallerServer` 同二进制挂载安装/激活服务（`internal/apps/offline/server/server.go`）。
- worker：异步任务走共享 DB/Redis，不靠 RPC（同端请求-响应才 RPC）。

## 4. 关联

- [[kapp-agent]]、[[pevent]]、[[kapp-web]]、[[kapp平台总览]]