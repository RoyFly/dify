# 配置变更清单

## docker/.env 参数变更

保留原有 244 个参数，其中修改 30+ 项（之前的1.8.1版本参考值同步及主机网络适配）；新增 8 个主机网络参数。

新增的 8 个主机网络参数：

| 参数 | 值 | 用途 |
| --- | --- | --- |
| `API_WEBSOCKET_PORT` | `5006` | WebSocket 独立端口。 |
| `AGENT_SSRF_HTTP_PORT` | `3129` | Agent 代理独立端口。 |
| `WEAVIATE_HTTP_PORT` | `18080` | Weaviate HTTP 监听端口。 |
| `WEB_PORT` | `3000` | Web 监听端口。 |
| `NGINX_LISTEN_ADDRESS` | `127.0.0.1` | Nginx 按参考部署仅监听本机。 |
| `NGINX_API_UPSTREAM` | `127.0.0.1:${DIFY_PORT:-5001}` | API 上游。 |
| `NGINX_WEB_UPSTREAM` | `127.0.0.1:${WEB_PORT:-3000}` | Web 上游。 |
| `NGINX_PLUGIN_UPSTREAM` | `127.0.0.1:${PLUGIN_DAEMON_PORT:-5002}` | 插件服务上游。 |


## 默认部署端口

仅列当前默认 profile（`weaviate,postgresql,collaboration`）及始终启动的服务，不包括替代 profile。

| 服务 | 端口 | 说明 |
| --- | --- | --- |
| Nginx HTTP | `20080` | 仅监听 `127.0.0.1`，入口为 `http://127.0.0.1:20080`。 |
| Nginx HTTPS | `20443` | 当前未启用 HTTPS；启用后仅监听 `127.0.0.1`。 |
| Web | `3000` | 仅监听 `127.0.0.1`。 |
| API | `5001` | 后端 HTTP 接口。 |
| WebSocket | `5006` | 工作流协作。 |
| Plugin daemon | `5002` | 插件服务。 |
| Plugin 调试 | `5003` | 插件远程调试。 |
| Agent backend | `5050` | Agent 服务。 |
| Local sandbox | `5004` | Agent 沙箱控制接口。 |
| PostgreSQL | `5432` | 主数据库。 |
| Redis | `6381` | 缓存和任务队列。 |
| Sandbox | `8195` | 代码执行接口。 |
| SSRF proxy | `3128` | 普通 HTTP 代理。 |
| Agent SSRF proxy | `3129` | Agent 专用代理。 |
| Weaviate HTTP | `18080` | 向量数据库 HTTP 接口，仅监听 `127.0.0.1`。 |
| Weaviate gRPC | `50051` | 向量数据库 gRPC 接口。 |

`worker`、`worker_beat`、`init_permissions` 不提供应用访问端口。主机模式使用进程实际监听端口，`EXPOSE_*` 不再执行端口映射。
