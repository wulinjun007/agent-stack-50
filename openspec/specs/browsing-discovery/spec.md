# browsing-discovery —— 浏览与发现能力

## ADDED Requirements

### Requirement: 客户端即时交互

榜单 SHALL 支持关键词搜索（匹配名称/仓库/一句话定位/调用说明）、7 分类过滤、排序切换（分类分组 · 按星 · 按最近活跃），全部在浏览器端完成，不发起任何网络请求。

#### Scenario: 中文关键词搜索

- **WHEN** 在搜索框输入「本地」
- **THEN** 定位或调用说明含「本地」的条目（如 ollama、LocalAI、open-webui） SHALL 即时保留，其余隐藏

#### Scenario: 组合过滤为交集

- **WHEN** 同时激活分类「部署与推理」与搜索词「MIT」
- **THEN** 可见条目 SHALL 为两条件交集，计数显示同步更新

#### Scenario: 排序不丢筛选状态

- **WHEN** 筛选与搜索处于激活态时切换排序
- **THEN** 筛选与搜索条件 SHALL 保持不变，仅条目顺序或分组方式变化

### Requirement: 结果计数守恒

任何筛选/搜索/排序状态下，页面 SHALL 显示"当前可见 N / 50"。

#### Scenario: 空结果可解释

- **WHEN** 搜索无命中
- **THEN** SHALL 显示空态提示与"清除筛选"操作，计数显示 0 / 50

### Requirement: 键盘与辅助技术可达

全部交互控件 SHALL 可键盘操作（Tab 聚焦、Enter 激活），焦点环 SHALL 瞬时出现且对比度 ≥ 3:1；详情展开 SHALL 使用原生 `details/summary` 或等效 ARIA 语义。

#### Scenario: 纯键盘走查

- **WHEN** 仅用 Tab/Enter 遍历页面
- **THEN** 搜索框、全部过滤 chips、每行展开/收起、外链 SHALL 均可触达并操作，焦点始终可见
