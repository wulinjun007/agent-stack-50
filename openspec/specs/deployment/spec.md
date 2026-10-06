# deployment —— 部署与分发能力

## ADDED Requirements

### Requirement: 四通道部署

项目 SHALL 提供并文档化四条部署通道：

1. GitHub Pages（主通道，main 分支根目录）；
2. 任意静态服务器 / Docker（`deploy/Dockerfile`，nginx:alpine，无构建步骤）；
3. Coolify / Dokploy 自托管 PaaS（识别仓库内 `deploy/docker-compose.yml` 直接拉起）；
4. 本地零依赖预览（`python3 -m http.server`）。

#### Scenario: 一条命令自托管

- **WHEN** 在装有 Docker 的机器上执行 `docker compose -f deploy/docker-compose.yml up -d`
- **THEN** 站点 SHALL 在本机 8080 端口可访问，镜像内 SHALL NOT 包含任何构建步骤

#### Scenario: Pages 公网可达

- **WHEN** 访问 `https://<owner>.github.io/agent-stack-50/` 及四条 hash 路由
- **THEN** 全部 SHALL 返回 HTTP 200 且内容完整渲染

### Requirement: 更新流程文档化

`README` SHALL 描述月度数据刷新流程：重跑核验 → 人工过差异 → 更新快照日期与期号（N6 报头期号行）→ 重新部署。

#### Scenario: 新维护者可独立完成一次刷新

- **WHEN** 按文档操作
- **THEN** SHALL 能在不咨询原作者的情况下完成一轮快照更新并部署
