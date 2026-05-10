# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 项目
Slay the Spire 2 游戏攻略站 — 海外用户，Google SEO 优先，Google AdSense 变现。

## 命令
```bash
npm install              # 安装依赖
npm run dev              # 开发服务器 (localhost:4321)
npx astro build          # 静态构建 → dist/
npx astro preview        # 预览构建产物
```

## 技术栈
- **Astro 6** + **Tailwind CSS 3** (通过 `@astrojs/tailwind` 集成)
- 纯静态输出 (SSG)，部署到 Vercel (GitHub 自动触发)
- 暗色主题: `bg-slate-900` / `text-slate-200`，强调色 `amber-400`
- `.npmrc` 设置 `legacy-peer-deps=true` — Astro 6 与 @astrojs/tailwind 存在 peer dep 冲突，**不要移除**

## 架构：页面即内容
所有内容直接内联在 `.astro` 文件中，没有外部 CMS 或 markdown 内容集合。新增页面 = 新增 `.astro` 文件。

```
src/
  layouts/BaseLayout.astro   # 全局布局 (SEO meta、AdSense、导航、页脚)
  pages/
    index.astro              # 首页 (模块卡片 + 简介)
    coop/
      index.astro            # 合作模式总览 (8 章节)
      character-combos.astro # 角色搭配 (7 章节 + 5x5 协同矩阵)
      card-synergies.astro   # 卡牌协同 (9 章节 + 4 级 Tier)
      boss-strategies.astro  # Boss 攻略 (7 章节)
      advanced-tips.astro    # 进阶技巧 (8 章节)
```

## 关键约束
- **多语言**: 网站支持 en/de/it/fr/es/ja/ko，但当前仅实现了英文。i18n 将使用 Astro 的文件路由 (`/de/coop/` 等)
- **AdSense**: `<script async src="...ca-pub-2441650437092903...">` 必须保持在 `<head>` 中 — 在 `BaseLayout.astro` 第 40 行
- **SEO**: 每个页面通过 `BaseLayout` 的 `title` 和 `description` props 注入独立 meta 标签、OG 标签、Twitter Card 和 canonical URL
- **开发者邮箱**: yuanye5939@gmail.com
