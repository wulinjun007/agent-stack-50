# Proposal: AgentStack 50 —— AI 工作流 · 智能体 · 部署 TOP50 年鉴站

## Why

Agent 工具生态选型噪音大：既有榜单数据失真（过期 star、错误许可、无视迁移改名），且只罗列不示范。需要一份逐仓核验、三条主线严格分组、并能示范"能力如何被调用"的工具栈年鉴站。

## What Changes

- 新增 `TOP50-榜单.md`：50 项目、7 分类，全部字段经 GitHub REST API 逐仓核验（2026-10-06/07 快照），含许可逐仓核对与停更标注。
- 新增 `PRD.md` 与本 `openspec/` 四件套：以规格驱动方式固化 4 个能力（ranking-data / browsing-discovery / capability-pipeline / deployment）。
- 新增 `index.html`：单文件静态站（榜单 + 能力管线 + PRD 阅读 + 数据口径），无构建、无外部 JS、无追踪。
- 新增 `deploy/`：Dockerfile + docker-compose + 四通道部署文档（Pages / Docker / Coolify·Dokploy / 本地）。

## Capabilities

### New Capabilities
- `ranking-data` —— 50 条核验数据的结构与快照可追溯性
- `browsing-discovery` —— 客户端搜索/过滤/排序
- `capability-pipeline` —— 7 层能力调用管线的展示与状态区分
- `deployment` —— 四通道部署与公网可达性

## Impact

- **Affected specs**: 全部为新增。
- **Affected code**: 仓库根新增 `index.html`、`TOP50-榜单.md`、`PRD.md`、`deploy/*`、`openspec/*`；无既有代码变更。
