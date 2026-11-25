---
tags:
  - kapp
  - proto
  - connect
  - 机制
created: 2026-11-16
---

# Proto 契约与代码生成

> 概念层见 [[平台 API 设计]]；本篇记 kapp ↔ kapp-agent 跨仓库契约的落地模型。
> 参与方：[[apiserver]]（服务端半）、[[kapp-agent]]（客户端半）、[[pevent]]（同仓共享）。

## 1. 超集/子集与复制方向

- kapp `api/pb`：超集（19 目录、7 服务，含 web/offline/agent 等）。
- kapp-agent `api/pb/agent/v1`：子集，4 个 proto —— `clusters / event / deploy_task_component / reg`。
- **复制方向：kapp → kapp-agent**（子集抄超集），手工双向同步，无共享 buf module；历史 commit 同日同主题双仓库提交。漂移风险靠纪律约束。
- 同仓库服务（apiserver↔pevent↔offline）共享一棵 `api/gen`，**只需一次生成**；生成次数 = 持有 proto 副本的仓库数，与服务数无关。

## 2. 生成：just proto = buf generate

各仓库 `just proto` 调 buf，Go 三插件产物：

| 产物 | 内容 | 谁用 |
|---|---|---|
| `*.pb.go` | 消息体：原生类型 + 字段编号 + 序列化（无行为） | 两侧都用 |
| `*_grpc.pb.go` | go-grpc 桩 | agent 服务里是**死代码**；third/centrifugo 里是**活代码**（见 [[双通道通信架构]]） |
| `agentv1connect/*.connect.go` | **客户端半 + 服务端半同文件** | 跨仓库各用一半 |

## 3. 两半模型：按角色分，不是按仓库分

以 `clusters.connect.go` 为例（两侧同构，仅 import 路径不同）：

- 客户端半：`NewClustersServiceClient(httpClient, baseURL)` → 方法 → `CallUnary` → `POST {baseURL}/kapp.agent.v1.ClustersService/SetAgentStatus`。
- 服务端半：`NewClustersServiceHandler(svc)` → Mount → switch procedure 常量 → 方法值 `svc.SetAgentStatus`。
- **kapp 用服务端半，agent 用客户端半**；同仓 pevent 直接 import kapp 的客户端封装 `internal/apps/apiserver/client`（共享 Clientset + Bearer 拦截器）。

会合点：两侧**逐字相同的 procedure 常量** + 同源 schema 描述符；跨语言（Go↔TS）对齐靠**字段编号**而非字段名。

## 4. 消息体的本质

proto 消息 = 数据形状（字段编号+类型）+ 序列化规则，**不含行为**；"调用"行为在 connect 桩里。所以"抄生成桩替代抄 proto"不可行：桩 import 本模块路径、绑定本仓库生成物，跨模块复制会编译断裂；必须抄 proto 重新生成。

## 5. TS 端差异（kapp-web）

- 一个生成文件同时含客户端+服务端+schema（connect-es 风格），无独立 `_grpc` 文件。
- 前端只消费客户端半与消息类型；SSE 推送的 JSON 帧靠字段名/编号与 Go 侧对齐。

## 6. 关联

- 调用实例 → [[组件部署流程]]、[[集群代理查询流程]]
- 通信协议层 → [[双通道通信架构]]；安全 → [[令牌与信封加密]]