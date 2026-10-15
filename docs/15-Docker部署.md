# Docker 部署

> **填写指南**：本文件回答「怎么用 Docker 打包、本地跑、生产跑」。镜像构建、Compose 编排、持久化、网络的通用规范。生产 Runbook 的具体命令在 `18-云服务器生产部署手册(模板).md`。

## 1. 镜像构建

> **填写指南**：Dockerfile 分阶段构建、基础镜像选择（Debian / Alpine / Distroless）、镜像体积优化。禁止使用 `:latest` tag 入生产。

- **基础镜像**：`<镜像与版本>`
- **多阶段构建**：`<是/否>`
- **安全扫描**：`<Trivy / Snyk 等>`

### 1.1 Dockerfile 骨架

```dockerfile
# syntax=docker/dockerfile:1
FROM <base-image>:<version> AS build
WORKDIR /app
# <构建步骤>

FROM <runtime-image>:<version>
WORKDIR /app
COPY --from=build /app/<artifact> ./
EXPOSE <port>
HEALTHCHECK --interval=30s CMD <check>
ENTRYPOINT ["<entry>"]
```

## 2. 镜像标签与版本

> **填写指南**：标签命名约定（`v<semver>` / `<sha>` / `<branch>`）、禁止 `latest` 入生产、镜像保留策略与清理周期。

## 3. Compose 编排

> **填写指南**：开发 / 测试 / 预发 / 生产 Compose 文件的继承与差异（`compose.yaml` + overlay）。健康检查、依赖关系、重启策略的统一约定。

### 3.1 关键服务编排

| 服务 | 镜像 | 端口 | 依赖 | 健康检查 |
| --- | --- | --- | --- | --- |

## 4. 持久化与卷

> **填写指南**：Volume vs Bind Mount 的选用；数据目录的权限管理；备份卷的位置与挂载。

| 挂载点 | 类型 | 用途 | 备份策略 |
| --- | --- | --- | --- |

## 5. 网络与端口

> **填写指南**：内部服务间网络、对外暴露的端口、反向代理（Caddy / Nginx / Traefik）的职责分工。

## 6. 环境配置注入

> **填写指南**：env file / Secrets / 配置中心的选用。密钥不入镜像、不入日志、不入版本控制。

## 7. 资源限制

> **填写指南**：CPU / 内存 / 磁盘 IO 的限制值；OOM 处理策略；日志滚动策略避免磁盘打爆。

## 8. 常用运维命令

> **填写指南**：日常运维高频命令（启停、日志、镜像清理、容器重建）。详细操作在 Runbook。

```bash
# <分类>
docker compose ps
docker compose logs -f <service>
docker compose up -d --build
docker system prune -af --volumes
```

## 9. 本地开发

> **填写指南**：本地 Compose 的最小化配置、热更新策略、开发用依赖的隔离。

## 10. 变更记录

| 版本 | 日期 | 变更说明 |
| --- | --- | --- |
| `<0.1.0>` | `<YYYY-MM-DD>` | `<初始化>` |
