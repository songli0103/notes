---
tags:
  - ai
  - agent
  - pi-agent
  - aiops
created: 2026-11-14
---

# 🤖 Pi-agent

> AI Agent 应用层：集群内智能运维助手（DaemonSet）——SSE 长连云平台，云端编排诊断任务，后期直连本地 vLLM。

## 定位

- 形态：装在客户集群的 agent（DaemonSet/Deployment）+ 云端控制面编排
- 通信：SSE 长连接到云平台（反方向的心跳/事件/任务流），通信机制见 [[03-Web 与 RPC]] 与 [[项目实践]]
- 演进：模型从云端 API → 本地 vLLM（OpenAI 兼容 API，客户端零改造）

## 主题清单（合并为一篇实战向大笔记）

### Agent 技术内核

- [[Tool Calling Function Calling]] — 工具定义（JSON schema）、LLM 循环调用、参数校验
- [[MCP 协议]] — Model Context Protocol 架构（client/server/transport）、与 Function Calling 的关系、SSE transport
- [[Agent Loop]] — ReAct 模式：规划 → 调工具 → 观察 → 循环；终止条件与最大步数
- [[Prompt 设计]] — 诊断 system prompt、结构化输出（JSON）、少样本示例
- [[本地模型对接]] — OpenAI 兼容客户端（→ [[03-vLLM]]）、流式输出处理、超时与降级

### AIOps 方法论

- [[AIOps 架构]] — 告警 → 上下文增强（logs/metrics/CMDB）→ 根因分析 → 行动（自动/人审）
- [[诊断工作流设计]] — 分层诊断（连 [[08-集群运维]] 排查方法论）、只读工具集、结果结构化
- [[k8sgpt]] — K8s 诊断 SRE 分析器：内置分析器、与 LLM 结合
- [[Kagent]] — CNCF 项目：Agent 即 K8s CRD、GitOps 管理 Agent
- [[Agent 安全]] — 只读优先、写操作 human-in-the-loop 审批、RBAC 最小权限、注入防护

### Pi-agent 架构解析

- [[Pi-agent 架构]] — DaemonSet 感知集群（Informer/watch）+ SSE 长连云平台 + 平台编排诊断任务
- [[数据支撑]] — 告警输入来自 [[Keep]]、观测数据来自 [[KPS]]/[[SigNoz]]

## 关联

- 原理基础 → [[07-API 与 Watch 机制]]（Informer/watch 是 agent 感知集群的基础）
- 诊断方法论 → [[08-集群运维]]（分层排查）
- 模型服务 → [[AI Infra]]（vLLM/Triton）
- 知识支撑 → [[RAG 与知识库]]
- 通信机制 → [[03-Web 与 RPC]]（SSE）、[[项目实践]]（agent 模式）
- 上游：[[AI 工程]]
