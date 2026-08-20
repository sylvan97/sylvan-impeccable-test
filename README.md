# Sylvan — Impeccable Test

Test project: Sylvan — 个人沉淀站（基于「impeccable design workflow」构建）

仓库描述：Test project: Sylvan — personal sedimentation site built via the impeccable design workflow. Astro + Supabase planned; dual visual directions (Field Notebook + Editorial Ink) with runtime theme switcher.

---

## 项目简介

这是一个个人静态/半动态沉淀站的测试工程，目标是使用 Impeccable 设计流程搭建一个具有两套视觉风格（Field Notebook 与 Editorial Ink），并支持运行时主题切换的站点。后续计划使用 Astro 构建，结合 Supabase 提供后端/数据层支持。

## 主要特色

- 双视觉方向：Field Notebook（手稿/笔记风）与 Editorial Ink（编辑/排版风）。
- 运行时主题/视觉切换（runtime theme switcher）。
- 以 Impeccable 设计流程为指导的组件与样式体系。
- 轻量静态页面为主，后续可接入 Supabase 提供内容管理或评论等功能。

## 技术栈（规划 & 当前）

- 规划：Astro（静态/混合渲染）、Supabase（后端/存储/认证）
- 当前仓库语言统计：HTML（100%）
- 可选/常见：TailwindCSS / CSS Modules / Typescript（视项目逐步引入）

## 目录（示例）

- /src — 源代码（页面、组件、样式）
- /public — 静态资源（图片、favicon）
- /scripts — 构建或工具脚本
- README.md — 项目说明

> 注意：以上为常见结构示例，实际结构以仓库当前内容为准。

## 本地开发（示例步骤）

下列命令为常见 Astro 项目流程示例，如果你采用 Astro，请根据实际 package.json 调整：

1. 克隆仓库
   git clone https://github.com/sylvan97/sylvan-impeccable-test.git

2. 安装依赖（若使用 npm）
   npm install

3. 本地开发
   npm run dev
   （或 `pnpm dev` / `yarn dev`，视包管理器而定）

4. 打包与预览
   npm run build
   npm run preview

Supabase（后续接入）：
- 在 Supabase 控制台创建项目
- 在仓库中通过环境变量（.env）配置 SUPABASE_URL 与 SUPABASE_ANON_KEY
- 在对应的服务端/客户端初始化 Supabase 客户端

## 设计与视觉方向切换

- 建议将两套视觉样式封装为独立的 CSS/主题配置（例如 CSS variables 或 Tailwind 主题扩展）。
- 运行时切换可通过在顶层 layout 中切换根类名或更改 CSS 变量实现，并持久化用户选择（localStorage / cookie）。

## 贡献

欢迎提交 Issue 或 Pull Request。贡献指南建议包括：
- 事项描述清晰（issue 模板）
- PR 包含变更说明与预览截图（如涉及 UI）
- 遵循项目的代码风格（格式化、lint）

## 许可证

默认建议：MIT（如果你有其他许可证偏好，请替换为相应许可证文本）

## 联系 / 作者

- GitHub: https://github.com/sylvan97

---
小提示：如果你希望 README 中加入英文版、徽章（build / license / stars）或展示站点截图/演示链接，我可以一并添加。
