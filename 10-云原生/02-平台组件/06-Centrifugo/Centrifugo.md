---
tags:
  - 平台组件
  - realtime
  - websocket
created: 2026-11-14
---

# 📡 Centrifugo

> 实时消息推送服务器（Go 编写）：平台向前端/客户端推送实时事件的通道——任务状态、告警通知、集群状态变更。

## 定位

- 语言无关的实时消息服务：客户端直连 Centrifugo，业务服务通过 API/gRPC 发布消息
- 支持 WebSocket / SSE / WebTransport 多种传输，天然适配浏览器和弱网客户端
- 与自建 SSE 网关的关系：Pi-agent 用 SSE 连云平台（推给平台的场景）；Centrifugo 解决「平台推给前端」的场景——两者方向互补

## 核心主题（合并为一篇实战向大笔记）

- [[连接与订阅模型]] — channel 机制、订阅权限、presence（在线状态）、历史消息
- [[JWT 鉴权]] — 连接 token 与订阅 token、过期与刷新
- [[服务端发布]] — HTTP API / gRPC proxy / Redis 引擎集成（Go 服务端怎么发消息）
- [[横向扩展]] — Redis / NATS 引擎、多节点一致性
- [[SSE 与 WebSocket 选型]] — 传输协议对比、代理与网关兼容性（nginx 转发注意事项）
- [[运维与容量]] — 连接数上限、内存/连接调优、监控指标

## 与平台的关系

- 云平台前端的实时事件通道（任务进度、告警推送）
- 与 [[项目实践]] 的 [[长连接与通信]] 主题交叉（SSE 管理是 Pi-agent 侧，Centrifugo 是前端侧）

## 相关

- 上游：[[平台组件]] · [[云原生]]
