---
description: 所有接口出错时返回统一的 4 字段错误结构。下表列出全部错误码与处置建议。
---

# 错误码

### 错误响应结构

所有错误响应（HTTP 4xx / 5xx）使用以下统一结构：

| 字段          | 类型      | 说明                              |
| ----------- | ------- | ------------------------------- |
| code int    | 业务码     | `0` = 成功；`!= 0` = 失败（见下表）       |
| data string | 机器可读错误码 | snake\_case，便于代码 switch / catch |
| msg string  | 人类可读消息  | 英文为准，可用于日志                      |

### 错误码表

| HTTP | error\_code              | 触发条件               | 建议处置                                 |
| ---- | ------------------------ | ------------------ | ------------------------------------ |
| 401  | api\_key\_invalid        | API Key 不存在或格式错误   | 检查 Header，确认 Key 完整复制                |
| 401  | api\_key\_disabled       | Key 已被禁用           | 前往 Dashboard 启用或更换 Key               |
| 401  | api\_key\_expired        | Key 已过期            | 前往 Dashboard 续期或重新创建                 |
| 402  | insufficient\_balance    | 钱包余额不足             | 前往 Dashboard 充值                      |
| 402  | product\_not\_subscribed | 当前账号未订阅该产品（套餐已到期等） | 续费或购买对应套餐；Key 本身仍有效                  |
| 422  | parameter\_invalid       | 请求参数格式或取值错误        | 按 message 修正参数；详见 OpenAPI            |
| 429  | rate\_limit\_exceeded    | 超出 QPS / 并发限制      | 参考 Retry-After header 退避重试           |
| 500  | internal\_error          | 服务端异常              | 附带 request\_id 反馈 support@novada.com |

#### Token 模式特有错误

| HTTP | error\_code    | 说明                                                    |
| ---- | -------------- | ----------------------------------------------------- |
| 401  | token\_invalid | access\_token 不存在或格式错误                                |
| 401  | token\_expired | access\_token 已过期（默认 7 天 TTL），重新调用 `/v1/oauth2/token` |
