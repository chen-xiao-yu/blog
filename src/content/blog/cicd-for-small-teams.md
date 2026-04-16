---
title: "从零搭建 CI/CD 流水线：小团队也能 DevOps"
description: "小团队如何用 GitHub Actions 搭建一套轻量但完整的 CI/CD 流水线，实现自动化测试、构建和部署。"
date: 2026-03-20
tags: ["CI-CD", "DevOps", "工具"]
---

## 为什么小团队需要 CI/CD？

很多小团队（1-5人）觉得 CI/CD 是大公司才需要的东西。但实际上，团队越小，CI/CD 带来的收益越大：

- **减少重复劳动** — 不再手动构建部署
- **防止低级错误** — 自动化测试把关
- **降低协作摩擦** — 代码风格自动检查
- **新人友好** — 流程即文档

## 技术选型

| 工具 | 用途 | 选择理由 |
|------|------|---------|
| GitHub Actions | CI/CD 平台 | 免费额度充足，与 GitHub 深度集成 |
| Docker | 容器化 | 环境一致性 |
| Netlify/Vercel | 前端部署 | 零配置，自动 HTTPS |

## 流水线设计

### 1. CI 阶段（Pull Request 触发）

```yaml
name: CI
on: pull_request
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-java@v4
        with:
          java-version: '17'
      - run: ./gradlew test
      - run: ./gradlew lint
```

### 2. CD 阶段（合并到 main 触发）

```yaml
name: Deploy
on:
  push:
    branches: [main]
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: ./gradlew build
      - uses: some-deploy-action@v1
```

## 实施步骤

### 第一步：代码规范检查
- 配置 ESLint / Checkstyle
- 加入 CI 流水线的第一步

### 第二步：自动化测试
- 单元测试覆盖率要求 > 60%
- 集成测试覆盖核心流程

### 第三步：自动部署
- 前端 → Netlify / Vercel
- 后端 → 云服务器 / 容器

### 第四步：通知
- 构建失败 → 飞书/钉钉群告警
- 部署成功 → 通知相关同学

## 常见坑

1. **环境变量泄露** — 敏感信息一定要用 GitHub Secrets
2. **缓存未配置** — 每次都重新下载依赖，浪费时间
3. **流水线太长** — 拆分成多个 Job 并行执行
4. **测试不稳定** — Flaky test 要及时修复或隔离

## 总结

小团队不需要搞复杂的 DevOps 体系。一条简单但可靠的 CI/CD 流水线，就能解决 80% 的效率问题。关键是先动起来，在实践中迭代。
