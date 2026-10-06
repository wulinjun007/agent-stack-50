# capability-pipeline —— 能力调用管线能力

## ADDED Requirements

### Requirement: 七层管线完整呈现

「能力管线」页 SHALL 按调研层、数据层、方法论层、设计层、实现层、QA 层、部署层七个层级（另有演进层）展示：该层调用了榜单中哪些项目、产出了什么工件；并 SHALL 配一张架构图。

#### Scenario: 架构图可读且可及

- **WHEN** 渲染管线架构图
- **THEN** 图 SHALL 为自包含 SVG（archify 式交付标准：无外部依赖、结构可验证），且携带 `role="img"` 与中文 `aria-label`

#### Scenario: 调用关系可跳转

- **WHEN** 访客点击管线中的项目名
- **THEN** SHALL 跳转到对应 GitHub 仓库，或站内榜单对应条目的展开锚点

### Requirement: 调用状态四分类

每个条目的调用方式 SHALL 标注且仅标注以下状态之一：**已调用**（本交付实际发生）、**方案已写**（工件已落盘 `deploy/`）、**路线图**（列入后续里程碑）、**参照**（方法论或样本引用）。

#### Scenario: 不把计划伪装成事实

- **WHEN** 展示任何条目的调用说明
- **THEN** 未实际发生的调用 SHALL NOT 使用完成时态描述，且 MUST 带四状态标注之一
