---
description: 每个 API Key 与账号有独立的 QPS 与并发配额。下文给出默认值、超限响应与重试策略。
---

# 限流

### 默认限制

| 产品                       | QPS（每 Key） | 并发（每账号）  |
| ------------------------ | ---------- | -------- |
| 代理 API（开放接口）             | 10         | —        |
| Scraper API              | 50         | 500（任务池） |
| Web Unblocker            | 30         | 100      |
| Browser API（HTTP 流量管理接口） | 10         | —        |

超限时返回 `HTTP 429 rate_limit_exceeded`，附 `Retry-After` header（秒）。客户端建议指数退避 + jitter 重试。

### 提升配额

升级套餐或联系 support@novada.com 申请定制配额。

