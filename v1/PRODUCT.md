# Product

<!-- impeccable:product-schema 1 -->

## Platform

web

## Stack

- **第一阶段（UI 确认）**：纯静态 HTML/CSS，多个独立 mockup 并行，用于选定方向。无框架、无构建工具、无依赖。
- **第二阶段（生产实现）**：Astro 最新版，所有依赖一律锁定无冲突的最新版本。
  - 文章数据源：GitHub 仓库，通过 Astro Content Collections 读取 markdown + frontmatter，不引入 CMS。
  - 旅记 / 相册 / citywalk 数据源：Supabase
    - 文本字段（标题、正文、日期、地点、描述）以行形式存储；
    - 媒体（照片、Live Photo、视频）走 Supabase Storage 公共 URL；
    - 优先构建时拉取做 SSG；动态查询场景走 SSR 路由。

## Language

- 仅中文（zh-CN）原创内容。
- 不搭 i18n 脚手架，不预留多语言路由。

## Audience & Sharing

- **公开、低压力**：任何访客都能看，无登录、无会员门槛。
- **暂无评论**：不在当前范围；如后续需要再单独讨论。
- **基础 SEO 与分享卫生**：标题、描述、og:image、canonical；不做激进的关键词/搜索排名优化。
- **可见性**：默认公开。私有/草稿分层当前不在范围。

## Persona

- 锚点名：**Sylvan**。
- 身份基调：**刻意抽象 / 氛围化**——不要求头像、不要求个人照、不要求社交账号露出。
- 站点语气跟随人格：安静、克制、有距离感；不是个人品牌舞台。

## Modules & Information Architecture

- `/` 首页：模块入口的着陆面，不做销售化包装。
- `/articles`（二级列表）→ `/articles/[slug]`（三级详情）
  - 重心是**文章的沉淀与展示**，阅读是首要任务，chrome 极简。
  - 内容来自 GitHub 仓库。
- `/travels`（二级列表）→ `/travels/[slug]`（三级详情）
  - 文字与媒体**等权重**；以地点 + 时间作为叙事锚点。
- `/albums`（二级，按 年 → 月 分组，**精选子集**）→ `/albums/[year]/[month]`（三级详情，**当月完整网格**）
  - 二级页只展示精选切片，附"查看更多"进入对应月份的完整三级页。
  - 同时支持静态照片、Live Photo、视频。
  - 三级页的呈现形式**可以是日历 UI**——按日期排布，每日单元格承载照片 / Live Photo / 视频；也可以采用常规网格。具体形态由 new-work 的视觉方向轮次决定。
- `/citywalks`（二级列表）→ `/citywalks/[slug]`（三级详情）
  - 路线驱动叙事；当与某条旅记同城市时可双向关联。
- **入口融合**：旅记 / 相册 / citywalk 在首页共享一个统一入口（具体命名由 new-work 决定），但**路由和地址仍各自独立、可被单独访问**。

## Data Sources

- **文章**：GitHub 仓库（markdown + frontmatter）→ Astro Content Collections。
- **旅记 / 相册 / citywalk**：Supabase
  - 文本字段做表；
  - 媒体走 Supabase Storage 公共 URL；
  - 静态化优先，动态场景走 SSR。

## Constraints（持久约束，后续工作必须保留）

- 所有文案以中文（zh-CN）撰写。
- 无评论、无反应、无社交互动组件。
- 人物保持抽象；在没有显式确认前，不得编造超出"Sylvan"之外的传记性细节。
- **视觉约束**（仅记录，不在此设计，留给 new-work）：gabrielbeaugonin.com —— 留白、简洁、交互克制、创意感。这是一个**约束**，不是成稿视觉。

## Open Decisions

- 无关键未决项。
- 已知留待实施阶段决定：相册"精选子集"的选取规则、Live Photo 播放方案、Supabase 表结构形状、相册三级页最终采用日历 UI 还是常规网格。
- 无障碍（a11y）目标级别尚未指定——目前按 web 内容默认基线（语义化、可键盘可达、合理对比度）执行，等需要时再升级。

## Out of Scope（明确不在范围）

- 评论、点赞、订阅、关注、用户账号。
- 多语言。
- 电商、付费墙、会员。
- 服务端用户行为追踪、广告投放。
