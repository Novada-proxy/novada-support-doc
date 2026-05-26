---
description: 所有接口出错时返回统一的错误结构。下表列出全部错误码与处置建议。
---

# 错误码

### 错误响应结构

所有错误响应使用以下统一结构：

| 字段          | 类型     | 说明                        |
| ----------- | ------ | ------------------------- |
| code int    | 业务码    | `0` = 成功；`!= 0` = 失败（见下表） |
| data string | 数据体    | 发生错误时，此字段为空               |
| msg string  | 人类可读消息 | 英文为准，可用于日志                |

### 错误码表

HTTP响应码统一使用200，处理时应根据业务错误码来判断具体的错误类型：

<table><thead><tr><th width="129">HTTP</th><th width="127">error_code</th><th>触发条件</th><th>建议处置</th></tr></thead><tbody><tr><td>200</td><td>50001</td><td>API Key 不存在或无效</td><td>检查 Header，确认 Key 完整复制</td></tr><tr><td>200</td><td>50002</td><td>Key 已被禁用</td><td>前往 Dashboard 启用或更换 Key</td></tr><tr><td>200</td><td>50003</td><td>Key 已过期</td><td>前往 Dashboard 续期或重新创建</td></tr><tr><td>200</td><td>500</td><td>服务端异常</td><td>附带 request_id 反馈 support@novada.com</td></tr></tbody></table>
