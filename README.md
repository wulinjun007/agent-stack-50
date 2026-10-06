# AgentStack 50 · AI 工作流 × 智能体 × 部署 GitHub TOP50 工具栈年鉴

> 第 001 期 · 数据快照 2026-10-07 · 50 项 / 7 分类 / Σ3,787,701★ · 逐仓核验

一份**逐仓核验**的 GitHub 高星工具栈年鉴：AI 工作流、智能体、部署三条主线的 TOP 50 开源项目。它同时是一次**能力调用示范**——本站的 PRD、视觉、QA 与部署本身就是用榜上工具（OpenSpec / Superpowers / hallmark / ui-skills / archify / Coolify / Dokploy …）的方法或工件做出来的，每个条目都标注了"本项目如何调用它"。

## 在线访问

- **GitHub Pages**：https://wulinjun007.github.io/agent-stack-50/
- 自托管 / 本地预览：见 [deploy/DEPLOY.md](deploy/DEPLOY.md)（四通道，含一条命令 Docker）

## 仓库结构

```
├── index.html          单文件站点（榜单 + 能力管线 + PRD + 数据口径，hash 路由）
├── TOP50-榜单.md        榜单正本（7 分类表 + 未入选说明 + 口径附录）
├── PRD.md              产品需求文档（12 章，含能力调用矩阵）
├── openspec/           OpenSpec 四件套：proposal / specs×4 / design / tasks
├── deploy/             Dockerfile · docker-compose.yml · DEPLOY.md（四通道）
├── QA-报告.md           hallmark 58 门禁 + 四视口 + 两段审查留痕
└── vendor/             本地参考用 skill 源码（hallmark/ui-skills，不入库）
```

## 数据口径（要点）

- Star / 语言 / 最近推送 / 许可标签来自 GitHub REST API 逐仓拉取，快照 **2026-10-06/07**；
- 许可一栏是**核验值**：GitHub 对自定义许可一律返回 NOASSERTION，本项目对 13 个存疑仓库逐个抓取 LICENSE 文件头部人工核对（如 AutoGPT = Polyform Shield + MIT 双许可、MCP 官方仓库正处 MIT→Apache-2.0 过渡）；
- 停更项（MetaGPT、autogen）显式标注；迁移/改名项（OpenHands、openclaude、lobehub）在条目内注明；
- 完整口径与排除项见站内「数据口径」页。

## 本地开发

无构建、无依赖：

```bash
python3 -m http.server 8080   # 或直接双击 index.html
```

月度刷新流程见 [deploy/DEPLOY.md](deploy/DEPLOY.md) 末节。

## License

榜单与站点内容：CC-BY-4.0（引用请注明快照日期与来源）。`vendor/` 内第三方代码各自遵循其原许可，不随本仓库分发。
