---
tags:
  - k8s
  - component
created: 2026-11-01
status: 已整理
---

# Kube-proxy

kube-proxy 负责在节点上**实现 Service 抽象**：它监听 Service 和 Endpoint 的变化，把「访问虚拟 IP → 转发到某个 Pod」的规则写到节点网络里。

## 它其实不「代理」流量

```mermaid
flowchart LR
    subgraph CONTROL["控制平面（写规则）"]
        KP["kube-proxy"] -->|"watch Service / Endpoint"| API["apiserver"]
    end
    KP -->|"写规则"| KERNEL["内核 iptables / IPVS"]
    TRAFFIC["真实流量"] -->|"直接走内核转发"| POD["后端 Pod"]
```

**架构思想——控制与数据分离**：kube-proxy 只写规则，真实流量由内核直接转发，不经过 kube-proxy 进程本身——所以它挂了短时间内流量也不断（规则还在内核里）。

## 三种工作模式

```mermaid
flowchart TB
    M["kube-proxy 模式"] --> U["userspace<br/>（已废弃）"]
    M --> I["iptables<br/>默认，规则链转发"]
    M --> IP["IPVS<br/>基于哈希表，性能更好"]
```

- **iptables**：把 Service 转成 iptables 规则链；规则很多时性能下降（线性匹配）。
- **IPVS**：内核级四层负载均衡（哈希表查找），大集群、高并发场景性能更好。

## 相关

- Service 是什么 → [[Service]]
- Service 如何找后端 → [[Endpoint 与 EndpointSlice]]
