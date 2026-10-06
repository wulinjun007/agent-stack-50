# Design: AgentStack 50

## Context

单维护者、零预算、需要长期可持续更新的静态年鉴。部署环境：GitHub Pages（主）+ 自托管 Docker（备）。数据体量固定为 50 条，全部可在客户端内存中处理。

## Goals / Non-Goals

- Goals：零依赖交付、断网可读（字体降级后）、无追踪、单文件可审计、月度可刷新。
- Non-Goals：实时数据、后端服务、用户系统、SEO 竞争性内容（内容本身即目的）。

## Decisions

### D1. 单文件 `index.html` 而非多页/框架

50 条数据 ≤ 60KB，客户端渲染毫无压力。单文件保证：无构建链、无依赖升级负担、`git blame` 即审计、任何静态服务器直接可跑。代价：PRD 需手工双写（md + 站内渲染），以「PRD.md 为源、站内页为渲染」纪律约束漂移。

### D2. 视觉采用 hallmark 纪律而非自由发挥

宏结构 13·Index-First（页面即清单）与内容形态完全同构；主题 Almanac（年鉴）自带"条目+细线+等宽数字"的参考书气质。全部 58 道门禁作为验收标准写进 QA 报告，而不是事后审美。

### D3. `details/summary` 作为条目展开

原生可折叠语义，零 JS 成本，键盘与读屏免费可用——比自研 accordion 少一类 ARIA 缺陷。

### D4. 许可字段用"核验值"而非 GitHub 标签

GitHub license API 对自定义许可一律返回 Other/NOASSERTION。本项目对 13 个存疑仓库逐个抓取 LICENSE 文件头部核对，得到"MIT 核心 + EE 目录""修改版 Apache-2.0""Polyform Shield 双许可"等真实结论。这是数据诚实性的关键差异点。

### D5. 数据嵌入为 JS 数组而非独立 JSON

独立 JSON 需 fetch，在 `file://` 下被 CORS 拦截。内联数组保证双击打开即可用。

## Risks / Trade-offs

- 单文件增长：V2 语义检索若引入向量化则突破单文件边界，届时拆 `assets/` 目录。
- 手工双写 PRD：接受；以 QA 报告中的"PRD 一致性检查"缓解。
- 中文长词搜索：50 条量级直接 `includes()` 即可，无需分词。

## Migration Plan

不适用（全新仓库）。

## Open Questions

- 月度刷新是否迁移到 n8n 自托管实例（需常驻宿主机）还是保持本机脚本？
- 语义检索的本地推理默认模型（GLM/Qwen 系列）待 V1.2 定。
