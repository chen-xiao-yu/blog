---
title: "如何用 React 构建一个现代化的个人博客"
description: "从零开始，使用 React + TypeScript + Vite 搭建一个具有文章列表、详情页、标签分类的个人博客网站。"
date: 2026-04-10
tags: ["React", "TypeScript", "前端"]
---

## 为什么选择 React？

React 是目前最流行的前端框架之一，拥有庞大的生态系统和丰富的社区资源。对于个人博客这种内容驱动的网站，React 的组件化思想能够很好地将页面拆分为可复用的模块。

## 技术选型

| 技术 | 用途 |
|------|------|
| React 18 | UI 框架 |
| TypeScript | 类型安全 |
| Vite | 构建工具 |
| Tailwind CSS | 样式方案 |
| React Router | 路由管理 |
| React Markdown | Markdown 渲染 |

## 项目结构

```
src/
├── components/    # 组件目录
│   └── Layout.tsx
├── pages/         # 页面目录
│   ├── Home.tsx
│   ├── Post.tsx
│   ├── Tags.tsx
│   └── About.tsx
├── data/          # 数据目录
│   └── posts.ts
└── types/         # 类型定义
    └── blog.ts
```

## 核心实现

### 路由配置

使用 React Router v6 的声明式路由：

```tsx
<BrowserRouter>
  <Routes>
    <Route path="/" element={<Layout />}>
      <Route index element={<Home />} />
      <Route path="/post/:id" element={<Post />} />
      <Route path="/tags" element={<Tags />} />
      <Route path="/about" element={<About />} />
    </Route>
  </Routes>
</BrowserRouter>
```

### Markdown 渲染

使用 `react-markdown` 库将 Markdown 内容渲染为 HTML：

```tsx
import ReactMarkdown from 'react-markdown';

function PostContent({ content }: { content: string }) {
  return <ReactMarkdown>{content}</ReactMarkdown>;
}
```

## 总结

搭建一个博客并不复杂，关键在于选择合适的技术栈并保持代码结构的清晰。后续可以考虑加入评论系统、搜索功能等增强体验。
