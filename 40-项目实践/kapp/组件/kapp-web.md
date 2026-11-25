---
tags:
  - kapp
  - web
  - 组件
  - 待深化
created: 2026-11-16
---

# kapp-web（组件卡，待深化）

> 定位：整体 B 的浏览器 UI；与 agent 同款 SSE 协议收推送，Connect/HTTP 上行。
> 参与流程：[[组件部署流程]]（进度呈现）。横切 → [[双通道通信架构]]、[[Proto契约与代码生成]]。入口 → [[kapp平台总览]]。

## 已知事实

- `src/store/sse/SSEService.ts`：单例；`url.searchParams.append('cf_connect', JSON.stringify(params))` + `new EventSource(url)`。
- 订阅 channel 形态 `gpt:web-event#<userid>`（`#` user-limited），token 由后端签发。
- TS 生成物：一个文件含客户端+服务端+schema（connect-es 风格），只消费客户端半。

## 待调研

- [ ] 上行 API 层（connect-es client 封装、鉴权 cookie/token）
- [ ] 部署进度页如何消费 ops_event/组件状态（SSE vs 轮询）
- [ ] 与 apiserver web 服务（超集 proto 的 web 目录）的对应关系

## 关联

- [[kapp平台总览]]、[[双通道通信架构]]、[[组件部署流程]]