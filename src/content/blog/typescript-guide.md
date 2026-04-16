---
title: "TypeScript 入门指南：类型系统完全解读"
description: "从 JavaScript 到 TypeScript，理解类型系统的核心概念，掌握泛型、联合类型、类型守卫等进阶技巧。"
date: 2026-04-02
tags: ["TypeScript", "前端", "编程语言"]
---

## 为什么学 TypeScript？

TypeScript 是 JavaScript 的超集，为动态类型的 JS 添加了静态类型检查。在大型项目中，类型系统能够：

- 🐛 在编译阶段发现错误
- 📖 提供更好的代码文档
- 🛠 增强 IDE 的自动补全和重构能力
- 🤝 提升团队协作效率

## 基础类型

```typescript
// 基本类型
let name: string = "张三";
let age: number = 25;
let isStudent: boolean = true;

// 数组
let scores: number[] = [90, 85, 92];
let names: Array<string> = ["张三", "李四"];

// 元组
let person: [string, number] = ["张三", 25];

// 枚举
enum Color {
  Red,
  Green,
  Blue
}
```

## 接口与类型别名

```typescript
// 接口
interface User {
  id: number;
  name: string;
  email?: string;        // 可选属性
  readonly avatar: string; // 只读属性
}

// 类型别名
type Status = "active" | "inactive" | "banned";
type UserWithStatus = User & { status: Status };
```

## 泛型

泛型是 TypeScript 最强大的特性之一：

```typescript
function first<T>(arr: T[]): T | undefined {
  return arr[0];
}

// 使用
first([1, 2, 3]);      // 类型推断为 number
first(["a", "b"]);     // 类型推断为 string

// 泛型约束
interface HasLength {
  length: number;
}

function logLength<T extends HasLength>(arg: T): T {
  console.log(arg.length);
  return arg;
}
```

## 类型守卫

```typescript
function process(value: string | number) {
  if (typeof value === "string") {
    // 这里 TypeScript 知道 value 是 string
    return value.toUpperCase();
  }
  // 这里 TypeScript 知道 value 是 number
  return value.toFixed(2);
}
```

## 实用工具类型

| 工具类型 | 作用 |
|---------|------|
| `Partial<T>` | 所有属性变为可选 |
| `Required<T>` | 所有属性变为必填 |
| `Pick<T, K>` | 从 T 中选取部分属性 |
| `Omit<T, K>` | 从 T 中排除部分属性 |
| `Record<K, V>` | 构造键值对类型 |

## 学习建议

1. 先掌握基础类型和接口
2. 理解泛型的概念和常用模式
3. 学会阅读 `@types` 声明文件
4. 在实际项目中逐步加深理解

不要试图一开始就写完美的类型——渐进式增强才是正确姿势。
