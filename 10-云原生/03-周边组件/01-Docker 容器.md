---
tags:
  - 云原生
  - docker
created: 2026-11-01
updated: 2026-11-14
---

# 🐳 Docker 容器

> 容器是整个云原生技术栈的底座——K8s 只是容器的编排层。写这篇时目标是把「容器到底是什么」讲透（namespace/cgroup/overlayfs），而不是罗列 Docker 命令。

## 主题清单（合并为一篇面试向大笔记）

- [[容器与镜像原理]] — namespace（隔离视图）/ cgroup（限制资源）/ overlayfs（分层文件系统）；容器 ≠ 虚拟机
- [[镜像分层与存储]] — 层复用、写时复制、镜像瘦身为什么有效
- [[Dockerfile 最佳实践]] — 指令顺序与缓存、非 root 用户、HEALTHCHECK
- [[多阶段构建]] — 编译期与运行期分离；Go 静态编译 + distroless/scratch
- [[容器网络基础]] — veth pair、bridge、端口映射原理（K8s 网络的前置知识）
- [[容器运行时对比]] — Docker / containerd / CRI-O；docker 与 K8s 的关系（dockershim 1.24 移除）

## 实战关联

- K8s 侧的运行时接口 → [[01-架构与组件]]（CRI 一节）
- 镜像构建进阶（ko / kaniko）→ [[09-生态与工具]]

## 相关

- 上游：[[云原生]]
