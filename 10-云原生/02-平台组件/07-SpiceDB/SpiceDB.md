---
tags:
  - 平台组件
  - authz
  - rebac
created: 2026-11-14
---

# 🔐 SpiceDB

> 开源关系型鉴权服务（Google Zanzibar 论文的开源实现）：平台多租户/细粒度权限的统一鉴权层。

## 定位

- 解决的不是「登录」（那是认证/IdP 的事），而是「谁对什么资源有什么权限」（授权）
- 模型是 ReBAC（基于关系）：把权限表达成资源之间的**关系图**（如 `team:platform#member@user:song`），而不是每用户配一遍权限
- 对比传统 RBAC：角色容易爆炸、层级资源难表达；Zanzibar 模型用递归关系图解决（文件夹树继承权限、团队嵌套）
- Go client 官方支持，gRPC API

## 核心主题（合并为一篇实战向大笔记）

- [[Zanzibar 论文精读]] — Google 的授权系统设计：关系元组、递归检查、一致性难题
- [[Schema 设计]] — 权限模型的 schema 语言：资源类型、关系、权限定义
- [[Relationship 写入]] — 关系元组的增删、一致性（zookie/时间戳防新旧不一致）
- [[Permission Check]] — Check API、Lookup Resources（我能看到哪些资源）、Lookup Subjects（谁能访问这个资源）
- [[一致性与性能]] — New Enemy Problem、缓存策略、P99 优化
- [[多租户设计]] — 每租户一个 permission system vs 前缀隔离
- [[与中间件的集成]] — Go SDK / gRPC / HTTP gateway；与 OPA/Casbin 对比选型

## 与平台的关系

- 云平台的统一鉴权层：多租户客户隔离、平台功能权限（谁可以管哪个集群、谁可以下发组件）
- 平台 API 的授权中间件 → [[平台 API 设计]]

## 相关

- 上游：[[平台组件]] · [[云原生]]
- 应用侧：[[项目实践]]
