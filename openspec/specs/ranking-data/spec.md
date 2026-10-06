# ranking-data —— 榜单数据能力

## ADDED Requirements

### Requirement: 固定规模与字段完备

站点 SHALL 内嵌恰好 50 条项目记录；每条记录 SHALL 包含：全局排名、名称、`org/repo`、分类（7 类之一）、star 数、主语言、许可、最近推送日期、一句话定位、入选理由、调用方式（含状态标注）、安装命令、仓库链接。

#### Scenario: 计数恒等

- **WHEN** 渲染榜单
- **THEN** 7 个分类条目数之和 SHALL 等于 50，且页面统计行的总星数为全部条目 star 之和（2026-10-06/07 快照为 3,787,701）

#### Scenario: 字段缺失即构建失败

- **WHEN** 任一条目缺少必填字段
- **THEN** 渲染层 SHALL 在控制台输出缺字段告警，且该条目不得以残缺形态上线

### Requirement: 快照可追溯

页面 SHALL 明示数据快照时间窗、数据源（GitHub REST API `GET /repos/{owner}/{repo}`）与许可核验方法（逐仓打开 LICENSE 文件人工核对）。

#### Scenario: 口径页可查证

- **WHEN** 访客打开「数据口径」
- **THEN** SHALL 看到快照日期、API 口径、许可核对说明、排除项清单（含未入选但 star 更高的项目及原因）

### Requirement: 停更与迁移诚实标注

- 最近推送距快照超过 6 个月的条目 SHALL 显示停更标记，且「为何入选」包含停更背景。
- 近一年内发生组织迁移或改名的条目（OpenHands、openclaude、lobehub）SHALL 在条目内注明迁移事实。

#### Scenario: 停更条目

- **WHEN** 查看 MetaGPT（最近推送 2026-01-21）或 autogen（2026-04-15）
- **THEN** 行内 SHALL 出现停更标记，展开后可见停更说明与历史地位入选理由
