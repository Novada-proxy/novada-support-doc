---
hidden: true
---

# 快速开始New

三步发出第一个请求：拿 Key → 加 Authorization Header → 调接口。

### 三步开始

1.  **注册 Novada 账号并获取 API Key**

    前往 [仪表盘-账号设置-我的账户-API Key](https://dashboard.novada.com/cn/api-key/) 创建一个 API Key。一个账号最多可创建 10 个 Key，可单独启停，最 长有效期 5 年，**支持永不过期**。
2.  **在 HTTP 请求头加入 Authorization**

    `Authorization: Bearer YOUR_API_KEY` —— 所有 API Key 类产品的接口都使用同一个 API Key，不再区分产品。**一 Key 通吃。**
3.  **发起你的第一次调用**

    下侧示例支持按语言切换。点击标签即可查看对应请求。响应中 `code: 0` 即表示成功。

GET /v1/wallet/balance

{% tabs %}
{% tab title="cURL" %}
```bash
# Method 1 · API Key direct (recommended)
curl -X POST https://api-m.novada.com/v1/wallet/balance \
  -H "Authorization: Bearer YOUR_API_KEY"

# Method 2 · Token Exchange (backwards-compatible)
TOKEN=$(curl -X POST https://api-m.novada.com/v1/oauth2/token \
  -H "Authorization: Bearer YOUR_API_KEY" \
  | jq -r .data.access_token)

curl -X POST https://api-m.novada.com/v1/wallet/balance \
  -H "Authorization: Bearer $TOKEN"
```
{% endtab %}

{% tab title="Python" %}
```python
# Method 1: direct
resp = requests.get(URL,
  headers={"Authorization": f"Bearer {API_KEY}"})

# Method 2: token exchange (legacy)
tok = requests.post("/v1/oauth2/token",
  headers={"Authorization": f"Bearer {API_KEY}"}
).json()["data"]["access_token"]
resp = requests.get(URL,
  headers={"Authorization": f"Bearer {tok}"})
```
{% endtab %}

{% tab title="Node.js" %}
```javascript
// Method 1: direct
const r1 = await fetch(url, {
  headers: { Authorization: `Bearer ${API_KEY}` }
});

// Method 2: token exchange (legacy)
const t = (await (await fetch('/v1/oauth2/token', {
  method: 'POST',
  headers: { Authorization: `Bearer ${API_KEY}` }
})).json()).data.access_token;
```
{% endtab %}

{% tab title="Go" %}
```go
// Method 1: direct
req.Header.Set("Authorization", "Bearer "+apiKey)

// Method 2: also Bearer, just the token
req.Header.Set("Authorization", "Bearer "+accessToken)
```
{% endtab %}

{% tab title="PHP" %}
```php
// Method 1: direct
curl_setopt($ch, CURLOPT_HTTPHEADER, [
  "Authorization: Bearer YOUR_API_KEY"
]);
```
{% endtab %}
{% endtabs %}

返回示例：

```json
{
    "code": 0,
    "data": {
        "balance": 168.1
    },
    "msg": "success",
    "timestamp": 1779677300
}
```

### 凭证模式

Novada 当前以 **API Key 直调** 为主路径。在 HTTP Header 中加入 `Authorization: Bearer YOUR_API_KEY` 即可发起调用，无 Token 过期问题、无需事先换取。

<details>

<summary>兼容保留：Token Exchange 模式（老用户无需改造）</summary>

原有的 Token Exchange 模式继续保留兼容：先调用 `/v1/oauth2/token` 换取 `access_token`（7 天 TTL），再用 token 调用业务接口。**现有代码无需改造**，但新项目建议直接使用 API Key 直调。

\# 方式 A（推荐）：API Key 作为 Bearer 直接换 token

curl -X POST https://api-m.novada.com/v1/oauth2/token \ -H "Authorization: Bearer YOUR\_API\_KEY"

\# 方式 B（兼容）：老的 Basic Auth (username:api\_key) 仍可用

curl -X POST https://api-m.novada.com/v1/oauth2/token \ -u "your\_username:your\_api\_key"

</details>
