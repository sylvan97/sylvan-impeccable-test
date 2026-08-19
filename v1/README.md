# Sylvan — 个人沉淀站（impeccable 测试项目）

> **测试中的项目**：用 [impeccable](https://github.com/...) 设计工作流做一个真实站点的完整设计过程。
> 当前处于**设计阶段**——产品事实 / 视觉方向已锁定，Astro 实现尚未开始。

## 这是什么

一个个人沉淀站，主线：**文章 / 旅记 / 相册（Live Photo & video）/ citywalk**。公开、低压力、无评论、无搜索、无标签云、无订阅——访客按时间序慢慢翻，或通过关联条目（citywalk ↔ 同城市旅记、旅记 ↔ 同月份相册、文章 ↔ 相关旅记）与 tag 聚合延展。

人格锚点：**Sylvan**，刻意抽象 / 氛围化，无头像无社交。语气安静、克制、有距离感。

## 技术栈（计划中，未实现）

- **Astro 最新版**（无冲突最新依赖）
- **文章**：GitHub 仓库 → Astro Content Collections
- **旅记 / 相册 / citywalk / tag**：Supabase（文本 + Storage 公共 URL）
- **媒体**：开源 CC0 / 自由许可素材（Unsplash / Pexels 等）

## 双视觉方向 + 运行时切换

本项目刻意锁定两个并列的视觉方向，由 Astro 实现层通过 `<html data-theme>` 切换：

| 方向 | 名称 | 角色 | Spec |
|---|---|---|---|
| A | **Field Notebook**（默认） | 手作笔记本 · 私人感 · 温度 | [`DESIGN-6-field-notebook.md`](./DESIGN-6-field-notebook.md) |
| B | **Editorial Ink**（备选） | 编辑印刷感 · 克制 · 文本为王 | [`DESIGN-1-editorial-ink.md`](./DESIGN-1-editorial-ink.md) |

索引与切换架构：[`DESIGN.md`](./DESIGN.md)

## 仓库结构

```
.
├── PRODUCT.md              ← 产品事实（平台 / 栈 / 受众 / IA / 约束）
├── BRIEF.md                ← 站点规划 brief（首页 / 模块 / 灵动岛 / States）
├── DESIGN.md               ← 设计索引（双锁定 + 切换架构）
├── DESIGN-6-field-notebook.md       ← 方向 A 锁定 spec
├── DESIGN-1-editorial-ink.md        ← 方向 B 锁定 spec
├── .impeccable/
│   ├── config.json         ← 工作流配置（buildPath: comp）
│   └── mocks/home/         ← 视觉方向候选 HTML mockup
└── README.md               ← 本文件
```

## 当前状态

- [x] 产品事实（PRODUCT.md）
- [x] 站点规划 brief（BRIEF.md）
- [x] 两个视觉方向锁定（DESIGN.md + 双 spec）
- [x] 首页双方向 mockup
- [ ] 其他 surface（articles / travels / albums / citywalks / tags）双方向实现
- [ ] Astro 项目脚手架
- [ ] 主题切换组件 + localStorage 持久化
- [ ] Supabase schema + 数据接入
- [ ] Live Photo / 视频播放方案

## License

MIT（待定，目前未指定）
