---
title: "JWT Token 深度解析：原理、实践与安全"
description: "全面解析 JSON Web Token 的工作原理、使用场景和安全最佳实践，帮助你在项目中正确使用 JWT。"
date: 2026-04-05
tags: ["JWT", "安全", "Java"]
---

## JWT 是什么？

JSON Web Token（JWT）是一种开放标准（RFC 7519），用于在各方之间安全地传输信息。它由三部分组成：

```
header.payload.signature
```

### 结构解析

**Header（头部）**
```json
{
  "alg": "HS256",
  "typ": "JWT"
}
```

**Payload（载荷）**
```json
{
  "sub": "1234567890",
  "name": "张三",
  "iat": 1516239022
}
```

**Signature（签名）**
```
HMACSHA256(
  base64UrlEncode(header) + "." + base64UrlEncode(payload),
  secret
)
```

## 工作流程

1. 用户登录，服务器验证身份
2. 服务器生成 JWT 并返回给客户端
3. 客户端在后续请求的 Authorization 头中携带 JWT
4. 服务器验证签名，提取用户信息

## 安全最佳实践

| 实践 | 说明 |
|------|------|
| 使用强密钥 | 至少 256 位随机字符串 |
| 设置过期时间 | 建议 Access Token 15分钟，Refresh Token 7天 |
| 不存敏感信息 | Payload 是 Base64 编码，不是加密 |
| 使用 HTTPS | 防止中间人攻击 |
| 验证 Issuer | 确保 Token 来自可信来源 |

## 常见问题

### Token 泄露怎么办？

- 缩短 Access Token 有效期
- 使用 Token 黑名单机制
- 绑定设备指纹

### 如何实现 Token 刷新？

使用双 Token 机制：
- **Access Token**：短期有效，用于 API 访问
- **Refresh Token**：长期有效，仅用于获取新的 Access Token

### 无状态 vs 有状态

JWT 的核心优势是无状态——服务器不需要存储 Session。但在某些场景下（如需要强制下线），仍需要引入状态管理。

## 总结

JWT 是一个强大的认证工具，但"能力越大责任越大"。正确理解其原理和安全边界，才能在项目中用好它。
