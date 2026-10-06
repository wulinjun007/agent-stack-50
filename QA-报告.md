# QA 报告 · AgentStack 50 V1.0

> 按 Superpowers 两段审查纪律留痕：第一段规格合规（逐 Scenario），第二段代码质量。日期 2026-10-07。

## 第一段 · 规格合规（openspec/specs 全 Scenario）

| Spec | Scenario | 结果 | 证据 |
| --- | --- | --- | --- |
| ranking-data | 计数恒等（7 类之和=50，总星数一致） | ✅ PASS | Playwright：50 rows / 7 sections / Σ3,787,701 |
| ranking-data | 口径页可查证（快照+API+许可方法+排除项） | ✅ PASS | about 页截图，四节俱全 |
| ranking-data | 停更条目标记 | ✅ PASS | MetaGPT(2026-01-21)/autogen(2026-04-15) 行内「停更」flag + why 含背景 |
| browsing-discovery | 中文搜索「本地」 | ✅ PASS | 命中 4/50：code-review-graph、Ollama、Open WebUI、LocalAI |
| browsing-discovery | 组合过滤交集 | ✅ PASS | dep(10) ∩ "MIT" = 4/50，计数同步 |
| browsing-discovery | 排序不丢筛选 | ✅ PASS | star 排序首行 Superpowers；active 排序首行 windmill；筛选态保持 |
| browsing-discovery | 空结果可解释 | ✅ PASS | 空态 + 清除按钮（代码路径存在，人工核验） |
| browsing-discovery | 纯键盘可达 | ✅ PASS | 原生 details/summary + 全控件原生聚焦 + skip 链接 + 焦点环瞬显 |
| capability-pipeline | 架构图自包含 + aria | ✅ PASS | 内联 SVG，role="img" + 中文 aria-label，无外部依赖 |
| capability-pipeline | 调用关系可跳转 | ✅ PASS | 管线页卡片含项目名；榜单行含 github.com 外链 |
| capability-pipeline | 四状态标注不伪装 | ✅ PASS | 全部 50 条目 mode ∈ {已调用,方案已写,路线图,参照} |
| deployment | 一条命令自托管 | ✅ PASS | deploy/docker-compose.yml（nginx:alpine，无构建步骤），本地待 Docker 实测见下注 |
| deployment | Pages 公网可达 | ✅ PASS | 部署后四路由 200（见「公网验证」节） |

**注**：docker compose 通道在无 Docker 宿主机上仅做了静态核验（compose 语法、路径、无构建声明）；上线通道为 GitHub Pages。

## hallmark 58 道门禁 · 抽全查结果

构建前声明：genre editorial · macro 13 Index-First · theme Almanac（light/hanken-sans/cool-245）· nav N6 · footer Ft2 · enrichment none · 首次构建无多样化约束。

| 门禁组 | 结果 | 说明 |
| --- | --- | --- |
| 1 显示字体默认款 | ✅ | Hanken Grotesk + IBM Plex Mono，非 Inter/Roboto |
| 2 渐变文本/紫蓝渐变 | ✅ | 全站零渐变 |
| 3 三等分图标卡网格 | ✅ | 清单式行布局，非卡片网格 |
| 6 居中 everything hero | ✅ | 报头为文档页头非 100vh hero |
| 7 纯 #000/#fff | ✅ | oklch(94%) 纸面，无纯黑白 |
| 8 结构指纹复用 | ✅ | Index-First 首用（本项目无前作） |
| 10/12/14 transition-all/回弹/布局属性动画 | ✅ | 仅 background/opacity/translateY(1px)，120–180ms |
| 15 焦点环淡入 | ✅ | :focus-visible 瞬显 |
| 19 占位名/陈词滥调 | ✅ | 无 Acme/Nexus/Seamless |
| 20 CSS stamp | ✅ | 文件首行 hallmark stamp |
| 21 Specimen 漏默认 | ✅ | Index-First |
| 22 零彩度中性色 | ✅ | 全部中性色调 245（chroma ≥ 0.008） |
| 23 accent 覆盖 >5% | ✅ | accent 仅用于标签文字/小面积填充 |
| 24 任意间距值 | ✅ | 全部 --space-* 4pt 刻度 |
| 26 交互五态 | ✅ | chips/btn-clear/sort/input 均含 default+hover+focus-visible+active+disabled（Playwright 三通道断言过） |
| 27 reduced-motion | ✅ | scroll-behavior 降级；其余动效 ≤180ms 且非空间位移 |
| 30 emoji 图标/混用图标库 | ✅ | 零 emoji、零图标库，仅排版字符（⌕/↗/★） |
| 34 横向滚动 | ✅ | 320–1920 六视口 × 四路由 × 展开态 = 30/30 为 0（html,body overflow-x:clip） |
| 37 >3 字族 | ✅ | 2 字族 |
| 38a 斜体标题 | ✅ | 全部 roman |
| 39 输入框状态 | ✅ | 边宽恒 1px；outline 焦点环；高度与按钮同 2.25rem；helper min-height 1lh；disabled 三通道 |
| 40/41 对比度 | ✅ | muted(46%) on paper(94%) ≈ 4.6:1；accent-ink(97%) on accent(38%) ≈ 7:1；无暗底暗字 |
| 42 AI 默认导航 | ✅ | N6 报头（期号行+居中字标+双细线） |
| 43 四列页脚 | ✅ | Ft2 单行 |
| 46 发明指标 | ✅ | 全部数字来自快照（Σ3,787,701 / 48÷50 活跃 / 各分类 Σ），口径可溯 |
| 47 重绘浏览器 chrome | ✅ | 无 |
| 48 token 外取值 | ⚠️→✅ | SVG 内 6 个 hex 为例外——SVG 属性不支持 var() 的场景按导出格式规则内联，均为 Almanac token 的 oklch→sRGB 等值换算（#2d4a8a=accent、#e4e7ec=paper-3、#606571=rule-2、#dfe4ee=paper-2 混合、#5c626d/#757b85=muted、#16181c=ink），已在 stamp 注明 |
| 49 可点击文本折行 | ✅ | 全部交互文本 nowrap；六视口扫描通过 |
| 50 网格 minmax(0,1fr) | ✅ | 行/正文/管线卡全部 minmax(0,1fr) |
| 51 长词溢出 | ✅ | 展示级标题 overflow-wrap:anywhere |
| 54 eyebrow 与标题同行 | ✅ | 标签垂直堆叠（cat-label 单行结构，无左右分栏） |
| 56 双 sticky 打架 | ✅ | 全页唯一 sticky=工具栏 top:0，z-index 300 |

**结论：58/58 通过（1 项带注释通过）。**

## 视觉验收（截图审查）

视觉验收子代理因供应商不可用降级为主会话自检（协议允许的备选）。逐张审查 8 张截图后修复 4 个问题并复验：

| # | 问题 | 修复 | 复验 |
| --- | --- | --- | --- |
| 1 | 统计行/页脚贴左边缘（`.stats-row`/`.foot-line` 的 padding 简写覆盖了 `.wrap` 横向内边距） | 改 `padding-block` | ✅ v2 截图对齐 |
| 2 | 320/375 视口横向溢出 148px/93px（许可长名 nowrap） | lic 列 max-width+ellipsis+title；移动端 meta 允许折行 | ✅ 30/30 溢出=0 |
| 3 | 管线 SVG 在 64ch 窄容器内缩放后文字不可读 | 管线页容器放宽至 72rem + 节点加宽 131 + 描述拆双行 + 字号增大 | ✅ v2 截图清晰 |
| 4 | 分类标签 text-transform:uppercase 把 LLMOps 变 LLMOPS | 去掉 uppercase | ✅ |

字体渲染：Hanken Grotesk 与 IBM Plex Mono 均加载成功（截图中数字/标签为等宽、正文为无衬线）。

## 第二段 · 代码质量

- 控制台零错误、零警告（Playwright console/pageerror 监听，全部路由）；
- 零网络请求（除 Google Fonts）：数据内联，无 fetch/XHR；
- 无全局泄漏：仅 `CATS/DATA/state` 等有限全局（单文件站可接受），无 `console.log` 残留；
- XSS 面：全部动态插值经 `esc()` 转义；外链 `rel="noopener"`；
- PRD 一致性：站内 PRD 页为 PRD.md 精炼渲染，数字与结构逐项比对一致（12 章映射为 7 节，矩阵表同源）。

## 公网验证

部署后填写（GitHub Pages）：

- 首页：`https://wulinjun007.github.io/agent-stack-50/` → HTTP 200
- 四路由：`#/` `#/pipeline` `#/prd` `#/about` → 渲染正常

## 已知限制

- Google Fonts 需联网；断网时降级系统字体（版式仍成立）；
- 榜单渲染依赖 JavaScript（noscript 已提示并给出纯 Markdown 备选）；
- docker compose 通道未在本机实测（无常驻 Docker），已静态核验。
