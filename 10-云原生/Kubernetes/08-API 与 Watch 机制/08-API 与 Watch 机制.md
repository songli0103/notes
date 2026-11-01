---
tags:
  - k8s
  - api-watch
  - moc
created: 2026-11-01
---

# 👁️ 08 API 与 Watch 机制

Kubernetes 最核心的内部机制：一切组件通过「监听 API Server 的变化」来协作。

## 主题

- [[API Server 请求处理流程]] — 认证 → 鉴权 → 准入 → 持久化
- [[resourceVersion 与乐观并发]] — 版本号与冲突处理
- [[List-Watch 机制]] — 先 List 全量，再 Watch 增量
- [[Informer 与工作队列]] — 客户端缓存 + 事件去重/分发的框架
- [[控制器与 Reconcile 循环]] — 期望状态 vs 当前状态的调谐
- [[OwnerReference 与垃圾回收]] — 级联删除的依赖关系
- [[Finalizer 机制]] — 资源删除前的清理钩子
- [[准入控制 Admission]] — Mutating/Validating Webhook
- [[CRD 与 API 扩展]] — 自定义资源与扩展 API

## 学习提示

这是理解 K8s 和写 Operator 的基石，与 [[Go 与 K8s 开发]] 强相关。建议顺序：[[resourceVersion 与乐观并发]] → [[List-Watch 机制]] → [[Informer 与工作队列]]（配合 [[client-go 入门]]）→ [[控制器与 Reconcile 循环]]。[[OwnerReference 与垃圾回收]] 和 [[Finalizer 机制]] 是写 Operator 时管理资源生命周期的必备。
