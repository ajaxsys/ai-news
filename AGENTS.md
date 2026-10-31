# AGENTS.md — ajaxsys/ai-news 内容公约

本仓库是个人主页的 AI 新闻公开数据（以后公开，GitHub Pages 服务）。维护本仓库的 AI Agent 须遵守以下规范。

## 目录结构

- `index.html` — 独立外壳（GitHub Pages 入口）：只含结构 + 样式 + 逻辑，不含任何新闻数据；先读 `news/manifest.json`，再按需加载对应日期 + 语言文件；数据失败时回退 jsDelivr 镜像；全站禁用 localStorage（语言/主题仅会话内状态）
- `news/manifest.json` — 唯一可信的日期列表：latest、updated_at、dates（新到旧）、editions
- `news/<date>.<lang>.json` — 每日每语言一个文件（`zh` / `en` / `ja`），单语言扁平格式
- `radar/` — 「玩法雷达」专栏（见下节）：`radar/index.html` 独立外壳 + `radar/manifest.json` + `radar/<date>.<lang>.json` 三语数据
- `AGENTS.md` — 本文件
- `README.md` — 仓库说明

## 数据格式铁律

每语言文件顶层：`{"date":"YYYY-MM-DD","edition":N,"items":[...]}`。

每条资讯必须包含以下五个字段，缺一不可：

| 字段 | 说明 |
|---|---|
| `title` | 标题（该语言） |
| `summary` | 1~2 行摘要（该语言） |
| `url` | 该条新闻的真实原始出处链接，必须可溯源，**绝不编造**；缺失时用 web 搜索补上 |
| `source` | 来源名称（如 Reuters、TechCrunch） |
| `category` | 三选一，按文件语言取值：中文 `实验室` / `开发者` / `研究`；英文 `Labs` / `Developers` / `Research`；日文 `ラボ` / `開発者` / `研究` |

## 更新规则

- 每天 11:51 同步：新增当日三语文件，更新 `manifest.json`（latest、dates、editions、updated_at 用真实时间）。
- `manifest.json` 是唯一可信的日期列表；主页外壳先读 manifest，再按需加载对应日期+语言文件。
- 不要删除历史日期文件（归档保留）。

## 玩法雷达专栏（radar/，2026-10-31 开设）

- 定位：每天侦察全网，只收录具体、可动手的新玩法/新项目（AI 远程控制、多 agent 编排、组网、Apple Silicon 本地模型与家庭算力、事件驱动常驻 agent、隔离放权；偶有标 `outside` 的「圈外」项）。背景与目的写在专栏页的「关于这个专栏」一节（三语）。
- 数据格式：`radar/<date>.<lang>.json` 顶层 `{"date":"YYYY-MM-DD","items":[...]}`；每条含 `title`、`summary`、`url`（一手来源）、`source`、`outside`（布尔）。`radar/manifest.json` 为唯一可信日期列表（latest、updated_at、dates 新到旧）。
- 更新规则：由玩法雷达每日任务（约 20:51 JST）在有够格条目时同步——新增当日三语文件并更新 manifest；没有够格条目则不更新（不凑数）。历史文件不删。
- **公开版铁律**：专栏面向公众，只写「是什么 + 出处」，**绝不出现只对维护者个人的适配分析（如「为什么适合你」）、私人基础设施细节（主机名、地址、内网信息）**。聊天推送版与公开版是两套文案，勿混。
- 外壳行为与主页一致：最近 3 天日期直接展示、其余收进下拉菜单；语言为点击展开下拉切换（zh / en / ja）；禁用 localStorage。外壳只含结构+样式+逻辑，不内嵌数据，数据失败时回退 jsDelivr。

## 外壳（index.html）

- 外壳不内嵌新闻数据；改 UI 只改 `index.html`，不动 `news/` 数据格式。
- 外壳的特集卡片（Issue 01/02）为硬编码内容，更新时随外壳一起改。
- 外壳的生成工具存私有仓库 `ajaxsys/muse` 的 `projects/ai-news-program/` 下（`build_shell.py` + `shell.js` + `test-harness.js`）；改完工具后重新生成并推送 `index.html`。

## 铁律

- **绝不 push 机密信息**：token、密钥、凭证等绝不写入本仓库（本仓库以后要公开）。
- 处理程序不在本仓库，存私有仓库 `ajaxsys/muse` 的 `projects/ai-news-program/` 下。
- 推送语言按文件语言（zh/en/ja）；专有名词不必硬译。
