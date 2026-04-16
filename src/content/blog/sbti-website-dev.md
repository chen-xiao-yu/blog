---
title: "SBTI 风格测试网站开发实录"
description: "记录从设计到开发一个 SBTI 风格测试网站的完整过程，包括技术选型、开发中遇到的坑和解决方案。"
date: 2026-03-28
tags: ["项目实战", "前端", "CSS"]
---

## 项目背景

SBTI（Science Based Targets initiative）风格的网站以其专业的数据展示和清晰的信息层级著称。本次开发旨在仿照 SBTI 官网的设计风格，构建一个具有类似视觉效果和交互体验的测试网站。

## 设计分析

### 视觉特征
- **配色**：以深蓝和绿色为主色调，传达专业和可持续发展的理念
- **排版**：大标题 + 简洁正文，层次分明
- **数据展示**：卡片式布局，数据可视化丰富
- **动效**：适度的滚动动画和过渡效果

### 信息架构
```
首页
├── Hero 区域 — 核心数据指标
├── 简介 — 使命与愿景
├── 统计 — 关键数字展示
└── 行动 — 参与方式

内页
├── 公司列表
├── 目标详情
└── 资源下载
```

## 技术实现

### 响应式设计

使用 CSS Grid 和 Flexbox 混合布局：

```css
.stats-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
  gap: 24px;
}
```

### 数据可视化

使用 CSS 实现简单的进度条和计数动画：

```css
.progress-bar {
  height: 8px;
  border-radius: 4px;
  background: linear-gradient(90deg, #10b981, #059669);
  animation: grow 1.5s ease-out;
}

@keyframes grow {
  from { width: 0; }
}
```

## 踩坑记录

### 1. 部署问题

部署时遇到了路径问题，SPA 应用在子路径下资源加载失败。

**解决方案**：在 Vite 配置中设置正确的 `base` 路径。

### 2. 字体加载

Google Fonts 在国内加载缓慢。

**解决方案**：使用 `font-display: swap` 并提供本地字体回退。

### 3. 动画性能

大量同时执行的动画导致页面卡顿。

**解决方案**：使用 `IntersectionObserver` 实现滚动触发，只在元素进入视口时启动动画。

## 总结

这次开发实践让我深入理解了专业级网站的设计思路。从视觉还原到性能优化，每一步都有新的收获。后续计划加入更多交互功能和真实数据对接。
