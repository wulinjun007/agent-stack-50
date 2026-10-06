# AgentStack 50 · 产品需求文档（PRD）

> **一句话定位**：一份逐仓核验的 GitHub 高星工具栈年鉴——收录 AI 工作流、智能体与部署三条主线的 TOP 50 开源项目，并示范"如何调用这些项目的能力"完成一次完整的交付。

| 文档信息 | |
| --- | --- |
| 版本 | V1.0 |
| 状态 | 已实现（V1 已交付并上线） |
| 日期 | 2026-10-07 |
| 数据快照 | 2026-10-06/07（GitHub REST API 逐仓核验） |
| 撰写方法 | 规格驱动开发（SDD），按 OpenSpec 目录与场景格式组织 |
| 配套物 | `openspec/`（proposal·specs·design·tasks 四件套）、`TOP50-榜单.md`、`index.html`（站点）、`deploy/`（部署工件）、`QA-报告.md` |

---

## 1. 背景与问题

AI Agent 工具生态在 2025–2026 经历了爆发：工作流编排、智能体框架、编码智能体、记忆系统、可观测、推理引擎、自托管 PaaS 各自长出几十个头部仓库。随之而来的是三个真实痛点：

1. **选型噪音**。"Awesome 清单"动辄上千条目、按字母排序、混杂营销型自荐条目，无法回答"这三天里我该装哪个"。
2. **数据失真**。转述文章里的 star 数、活跃度、许可信息普遍过期或错误；同名迁移（OpenHands 换组织、openclaude 换社区、lobe-chat 改名）让二手信息更不可信。
3. **只列不用**。绝大多数榜单止步于罗列，不回答"这些工具到底怎么在一个真实项目里被调用"。

**我们的位置**：用 GitHub API 逐仓核验的实时数据 + 三条主线（工作流/智能体/部署）的严格分组 + 一份"本项目就是用这 50 项的能力做出来"的调用管线，把榜单从"目录"升级为"示范"。

## 2. 目标用户与核心场景

| 用户 | 场景 | 站内动作 |
| --- | --- | --- |
| 选型工程师 | 为团队搭建 agent 工作流，需在 n8n/dify/langflow 间做取舍 | 按「工作流编排」分类过滤 → 看许可与活跃度 → 展开「为何入选/如何调用」 |
| 技术决策者 | 评估自托管部署路线（内网/私有化） | 直达「部署与推理」分类 → 看 Coolify/Dokploy/Ollama 组合 → 照 `deploy/DEPLOY.md` 落地 |
| 学习者 | 想系统了解 agent 工程的全景 | 读「能力管线」页 → 从 OpenSpec/Superpowers/hallmark 逆向学习整套方法论 |

## 3. 产品定位与设计原则

**定位**：年鉴式工具栈榜单（Almanac）——冷静、可核验、可复现。

1. **真实数据**：所有 star/活跃/许可数据来自 GitHub REST API 逐仓拉取，标注快照日期；许可疑难点（NOASSERTION）逐仓打开 LICENSE 文件核对。
2. **诚实呈现**：不发明指标；停更项目（MetaGPT、autogen）入选必须标注停更事实与入选理由。
3. **能力调用**：每个条目回答"本项目如何调用它"；站点自身的 PRD、设计、QA、部署就是调用示范。
4. **无 slop**：视觉按 hallmark 纪律构建（宏结构 13·Index-First × 主题 Almanac × 58 道门禁），文案不使用营销套话。
5. **零依赖交付**：单文件 `index.html`，无构建步骤、无外部 JS、无追踪；断网（字体降级后）仍完整可读。

## 4. 范围

**V1 做**：50 项目榜单（7 分类、搜索、排序、筛选、展开详情）、能力管线页（含架构图）、PRD 阅读页、数据口径页、四通道部署工件。

**V1 不做**：实时数据自动刷新（走月度人工刷新流程）、语义检索、用户系统、评论、非 GitHub 数据源。

## 5. 信息架构

```
index.html（单文件 SPA，hash 路由）
├── #/          榜单    —— 50 项 × 7 分类，搜索/排序/筛选，行内展开详情
├── #/pipeline  能力管线 —— 7 层调用管线 + 架构图（archify 式交付标准）
├── #/prd       PRD    —— 本文档的站内渲染
└── #/about     数据口径 —— 快照方法、许可口径、排除项、已知风险
```

## 6. 需求规格（OpenSpec 场景式）

> 完整机器可读版本见 `openspec/specs/`，此处为同等内容的可读渲染。格式约定：`SHALL` 表强制项，`WHEN/THEN` 表验收场景。

### 6.1 榜单数据（ranking-data）

**Requirement**：站点 SHALL 内嵌恰好 50 条项目记录，每条含：全局排名、名称、`org/repo`、分类、star 数、主语言、许可、最近推送日期、一句话定位、入选理由、调用方式、安装命令、仓库链接。

- **Scenario** 数据快照可追溯
  - **WHEN** 访客打开「数据口径」页
  - **THEN** 页面明示快照时间窗（2026-10-06/07）、数据源（GitHub REST API `GET /repos/{owner}/{repo}`）、许可核验方法（LICENSE 文件逐仓人工核对）
- **Scenario** 停更项目诚实标注
  - **WHEN** 某条目最近推送距快照超过 6 个月
  - **THEN** 该行 SHALL 显示停更标记，且「为何入选」必须包含停更背景（如 MetaGPT、autogen）
- **Scenario** 总量守恒
  - **WHEN** 筛选、搜索、排序状态变化
  - **THEN** 结果计数 SHALL 同步显示"当前可见 N / 50"，不出现隐性丢失

### 6.2 浏览与发现（browsing-discovery）

**Requirement**：榜单 SHALL 支持三类即时交互——关键词搜索（匹配名称/仓库/定位/标签）、分类过滤（7 类多选）、排序切换（分类分组·按星·按活跃），全部客户端完成、无网络请求。

- **Scenario** 搜索中文关键词
  - **WHEN** 在搜索框输入「本地」
  - **THEN** ollama、LocalAI、open-webui 等定位含"本地"字样的条目即时保留，其余隐藏
- **Scenario** 组合过滤
  - **WHEN** 同时激活分类「部署与推理」与搜索「MIT」
  - **THEN** 结果为两条件的交集，计数同步更新
- **Scenario** 排序切换不丢状态
  - **WHEN** 用户在筛选激活状态切换排序
  - **THEN** 筛选条件保持，仅顺序/分组变化

### 6.3 能力调用管线（capability-pipeline）

**Requirement**：「能力管线」页 SHALL 按 7 个层级（调研→规格→方法论→设计→实现→QA→部署，外加演进层）展示每个层级调用了榜单中哪些项目、产出了什么，并配一张可读架构图。

- **Scenario** 调用关系可验证
  - **WHEN** 访客点击管线中任一项目名
  - **THEN** SHALL 能跳转到对应仓库或站内条目展开位
- **Scenario** 已调用与路线图区分
  - **WHEN** 展示某条目的调用方式
  - **THEN** SHALL 明确标注「已调用 / 方案已写 / 路线图 / 参照」四种状态之一，不得把计划伪装成事实

### 6.4 部署与分发（deployment）

**Requirement**：项目 SHALL 提供四条部署通道并全部文档化：① GitHub Pages（主通道）；② 任意静态服务器（`deploy/Dockerfile` + `docker-compose.yml`）；③ Coolify / Dokploy 自托管 PaaS 拉起；④ 本地零依赖预览（`python3 -m http.server`）。

- **Scenario** 一条命令自托管
  - **WHEN** 在装有 Docker 的机器上执行 `docker compose -f deploy/docker-compose.yml up -d`
  - **THEN** 站点 SHALL 在 8080 端口可访问，且容器内不含任何构建步骤
- **Scenario** Pages 公网可达
  - **WHEN** 部署到 GitHub Pages 后访问 `https://<user>.github.io/agent-stack-50/`
  - **THEN** 首页 SHALL 返回 200 且四条路由均可直达

## 7. 能力调用矩阵（本 PRD 的核心差异化章节）

> 「调用这些项目的能力」不是修辞——下表是本项目对 50 项中每个条目的真实使用方式。状态四种：**已调用**（本交付中实际发生）、**方案已写**（工件已落盘于 `deploy/`）、**路线图**（列入 V1.1/V2）、**参照**（方法论/样本引用）。

| 层级 | 调用的项目 | 状态 | 说明 |
| --- | --- | --- | --- |
| 调研层 | awesome-mcp-servers、modelcontextprotocol/servers | 已调用 | MCP 生态索引过滤官方标记后确定接入面；MCP 参考实现作为外部能力接入规范 |
| 数据层 | GitHub REST API（非榜单项）、OpenSpec | 已调用 | 63 个候选仓逐仓拉取 star/语言/许可/活跃；PRD 按其目录与 SHALL/WHEN/THEN 格式落盘 |
| 方法论层 | Superpowers | 已调用 | 构建走其阶段流：需求梳理→任务拆解→实现→两段审查（规格合规+代码质量）；`QA-报告.md` 即第二段审查产物 |
| 设计层 | hallmark、ui-skills | 已调用 | 本站 = Almanac 主题 × Index-First 宏结构 × 58 道 slop 门禁全过；元数据/可访问性按 ui-skills 对应检查单执行 |
| 实现层 | archify（交付标准） | 已调用（式） | 管线架构图按其标准手写：自包含、可交互、结构可验证、带 aria |
| QA 层 | browser-use（同类能力）、SkillSpector | 已调用 | Playwright 无头截图 + 视觉验收；第三方 skill 采纳前人工审读源码（与 SkillSpector 同思路） |
| 部署层 | coolify、dokploy、ollama、open-webui、litellm、anything-llm、vllm、LocalAI、ray | 方案已写 / 路线图 | 四通道部署见 `deploy/DEPLOY.md`；推理组合（ollama+open-webui / vllm+ray / LocalAI / litellm 网关）按规模分层选型 |
| 运营层 | n8n、activepieces、windmill、paperclip、gastown、OpenHands | 路线图 | 月度数据刷新流水线与"心跳+原子任务"维护机制的候选 |
| 演进层 | mem0、hindsight、graphiti、langfuse、opik、langchain、langgraph、llama_index、dify | 路线图 | 个性化记忆、知识图谱、评测观测、语义检索的分层候选 |
| 剩余条目 | AutoGPT、MetaGPT、autogen、crewAI、Flowise、langflow、smolagents、agno、adk-python、openai-agents、lobehub、cua、kimi-code、openclaude、K-Dense、ai-agent-book、code-review-graph、hallmark（参照位）等 | 参照 | 框架对照物与历史坐标，服务选型决策 |

## 8. 设计系统（hallmark 纪律的落地）

- **流派/宏结构/主题**：editorial · 13 Index-First · Almanac（冷调纸面 oklch(94% .008 245) + 石板蓝 accent oklch(38% .135 250) + Hanken Grotesk / IBM Plex Mono，共 2 个字族）
- **导航/页脚**：N6 报头式（期号行 + 居中字标 + 双细线）/ Ft2 单行版权行——避开 AI 默认导航与四列页脚指纹
- **硬性规则**：`html,body{overflow-x:clip}`；交互元素五态齐备（含 disabled 三通道）；输入框边宽恒定、焦点环瞬显；动效只碰 background/opacity 且 `prefers-reduced-motion` 降级；零渐变文本、零 emoji 图标、零重绘浏览器 chrome；eyebrow 与标题垂直堆叠；每个 sticky 位唯一
- **文案**：统计数字全部来自快照数据；无" trusted by"式发明

## 9. 部署与运维

主通道 GitHub Pages（main 分支根目录）；自托管通道 Dockerfile（nginx:alpine）与 docker-compose（8080 端口）；Coolify/Dokploy 识别仓库内 compose 直接拉起；本地预览 `python3 -m http.server`。更新流程：月度重跑核验脚本 → 人工过差异 → 更新快照日期与期号 → 重部署。可观测（langfuse/opik）与个性化（mem0/hindsight）在语义检索功能上线后引入。

## 10. 验收标准（摘要）

1. 50 条数据与 `TOP50-榜单.md` 完全一致，计数恒等式通过（7 类之和 = 50）。
2. hallmark 58 道门禁全过（QA 报告逐条记录）。
3. 四视口（320/375/768/1280）无横向滚动、无可折行点击文本。
4. 四条 hash 路由 + 搜索/筛选/排序全部可用，键盘可达（Tab/Enter/焦点环）。
5. 部署后公网四路由 200。
6. 两段审查（规格合规 + 代码质量）均留痕于 `QA-报告.md`。

## 11. 里程碑

| 里程碑 | 内容 | 状态 |
| --- | --- | --- |
| V1.0 | 50 项目榜单 + PRD + 单文件站 + 四通道部署工件 | ✅ 2026-10-07 交付 |
| V1.1 | 月度刷新脚本（GitHub API diff 报告）+ 停更自动标记 | 规划中 |
| V1.2 | 语义检索（ollama + llama_index 本地方案优先）+ langfuse 观测 | 规划中 |
| V2.0 | 项目关系图谱（graphiti）+ 个性化记忆（mem0）+ 订阅通知（activepieces） | 远期 |

## 12. 风险与开放问题

- **数据时效**：star 数日变动数千属常态，页面以快照日期自我声明，不做实时承诺。
- **仓库迁移**：OpenHands、openclaude、lobehub 一年内均发生迁移/改名；月度刷新需检测 301。
- **许可变动**：MCP 官方仓库正处于 MIT→Apache-2.0 过渡；n8n/dify/lobehub 等自定义许可商用前须逐条读条款。
- **维护成本**：若转入月度自动刷新，需评估 n8n/paperclip 路线与本机 Node 版本约束（paperclip 需 Node ≥ 24）。
