# Tasks: AgentStack 50

> 按依赖排序；勾选即完成。任务粒度遵循"单任务 ≤ 一次专注会话"原则（Superpowers 拆解纪律）。

## 1. 数据层（ranking-data）

- [x] 1.1 从既有核验记忆（36 仓）+ GitHub API 补充候选至 63 仓，拉取 star/语言/许可/活跃
- [x] 1.2 按工作流/智能体/部署三主线分组，定版 TOP50（7 分类）
- [x] 1.3 对 13 个 NOASSERTION 许可仓逐个核对 LICENSE 文件头部
- [x] 1.4 标注停更项（MetaGPT/autogen）与迁移项（OpenHands/openclaude/lobehub）

## 2. 规格层（OpenSpec）

- [x] 2.1 写 `openspec/proposal.md`（Why/What/Capabilities/Impact）
- [x] 2.2 写 4 个 capability spec（SHALL + WHEN/THEN 场景）
- [x] 2.3 写 `design.md`（5 项决策 + 权衡）与 `tasks.md`

## 3. 文档层

- [x] 3.1 `PRD.md`（12 章，含能力调用矩阵）
- [x] 3.2 `TOP50-榜单.md`（7 分类表 + 口径附录）

## 4. 实现层

- [x] 4.1 hallmark 纪律加载：SKILL.md + Index-First 宏结构 + Almanac token + 58 门禁
- [x] 4.2 构建 `index.html`：N6 报头 / 工具栏 / 7 分类 50 行 / 管线页 / PRD 页 / 口径页
- [x] 4.3 元数据按 ui-skills fixing-metadata 检查单补齐（OG/Twitter/JSON-LD/canonical）

## 5. 部署层（deployment）

- [x] 5.1 `deploy/Dockerfile` + `deploy/docker-compose.yml`
- [x] 5.2 `deploy/DEPLOY.md`（四通道 + 月度刷新流程）

## 6. QA 层（两段审查）

- [x] 6.1 第一段（规格合规）：逐条核对本 spec 的全部 Scenario
- [x] 6.2 hallmark 58 门禁逐条过 + 四视口截图（320/375/768/1280）
- [x] 6.3 第二段（代码质量）：JS 无全局泄漏、无网络请求、无 console 残留
- [x] 6.4 `QA-报告.md` 落盘
- [x] 6.5 GitHub Pages 部署 + 公网四路由 200 验证
