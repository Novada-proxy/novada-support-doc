---
hidden: true
---

# 快速开始

***

### 概述

欢迎使用 Novada Public API。本文档提供了与 Novada 平台进行程序化交互的完整接口说明。通过本 API，您可以安全、高效地管理和调用平台的计算与代理服务。

#### 快速入门

使用Novada Public API需要获取使用凭证，保证调用安全

步骤：

1. 获取凭证：[登录Novada控制台—账号设置—我的账户—API Key](https://dashboard.novada.com/cn/api-key/)，获取您的 `用户名` 和 `API Key`(API Key支持更换)
2. 获取调用令牌：使用Public API需要获取`access_token`，以便于调起每次请求\
   `access_token`（默认有效期7天，需要及时更换或部署自动化更换程序)\
   使用您的凭证调用认证接口，换取一个 `access_token`
3. 发起调用：在请求头中携带该令牌，即可调用其他业务接口。

示例：创建一个代理账户

```
# 步骤2. 获取访问令牌
curl -X POST https://api-m.novada.com/v1/oauth2/token \
  -u "your_username:your_api_key"

# 步骤3. 使用令牌创建资源（假设返回的令牌是 “eyJhbG...”）
curl -X POST https://api-m.novada.com/v1/proxy\_account/create \
  -H "Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..." \
  -H "Content-Type: application/json" \
  -d '{"name": "my_agent", "type": "standard"}'
```

***

#### 获取访问令牌

请求`POST https://api-m.novada.com/v1/oauth2/token`

认证方式：HTTP Basic Authentication

* 用户名：您的 Novada API 用户名
* 密码：您的 Novada API Key

响应示例

```
{
  "code": 0,
  "data": {
    "access_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
    "expires_in": 604800,
    "token_type": "bearer"
  },
  "msg": "success",
  "timestamp": 1747036799
}
```

#### 使用访问令牌

获取令牌后，将其包含在所有后续 API 请求的 `Authorization` 头中：

```
POST https://api-m.novada.com/v1/proxy_account/create
Authorization: Bearer <access_token>
```

#### 安全最佳实践

1. 保护凭证：API 密钥等同于密码，请勿在客户端代码或公开仓库中暴露。
2. 令牌存储：将访问令牌存储在服务端的安全内存或加密存储中。
3. 及时轮换：定期在控制台中轮换您的 API 密钥，尤其是在怀疑泄露时。

***
