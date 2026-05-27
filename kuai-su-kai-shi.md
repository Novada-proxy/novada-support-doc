# 快速开始

三步发出第一个请求：拿 Key → 加 Authorization Header → 调接口。

{% stepper %}
{% step %}
### 注册 Novada 账号并获取 API Key

前往 [**仪表盘 - 账号设置 - 我的账户 - API Key**](https://dashboard.novada.com/cn/api-key/) 创建一个 API Key。单账号最多可创建 10 个 Key，可独立启停，最长有效期 5 年，**支持永不过期**。
{% endstep %}

{% step %}
### 在 HTTP 请求头加入 Authorization

```http
Authorization: Bearer YOUR_API_KEY
```

所有 API Key 类产品的接口都使用同一个 API Key，不再区分产品。**一 Key 通吃。**
{% endstep %}

{% step %}
### 发起你的第一次调用

下方示例按语言切换，调用 `GET /v1/wallet/balance` 查询账户余额，响应中 `code: 0` 即表示成功。
{% endstep %}
{% endstepper %}

### 示例：查询账户余额

`GET https://api-m.novada.com/v1/wallet/balance`

{% tabs %}
{% tab title="cURL" %}
```bash
curl -X GET https://api-m.novada.com/v1/wallet/balance \
  -H "Authorization: Bearer YOUR_API_KEY"
```
{% endtab %}

{% tab title="Python" %}
```python
import requests

resp = requests.get(
    "https://api-m.novada.com/v1/wallet/balance",
    headers={"Authorization": "Bearer YOUR_API_KEY"},
)
print(resp.json())
```
{% endtab %}

{% tab title="Node.js" %}
```javascript
const res = await fetch("https://api-m.novada.com/v1/wallet/balance", {
  headers: { Authorization: "Bearer YOUR_API_KEY" },
});
console.log(await res.json());
```
{% endtab %}

{% tab title="Go" %}
```go
req, _ := http.NewRequest("GET",
  "https://api-m.novada.com/v1/wallet/balance", nil)
req.Header.Set("Authorization", "Bearer YOUR_API_KEY")

resp, _ := http.DefaultClient.Do(req)
defer resp.Body.Close()
```
{% endtab %}

{% tab title="PHP" %}
```php
$ch = curl_init("https://api-m.novada.com/v1/wallet/balance");
curl_setopt($ch, CURLOPT_HTTPHEADER, [
    "Authorization: Bearer YOUR_API_KEY",
]);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
$response = curl_exec($ch);
curl_close($ch);
```
{% endtab %}
{% endtabs %}

**成功响应：**

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

Novada 当前以 **API Key 直调** 为主路径——在 HTTP Header 中加入 `Authorization: Bearer YOUR_API_KEY` 即可发起调用，无 Token 过期问题、无需事先换取。

<details>

<summary>兼容保留：Token Exchange 模式（老用户无需改造）</summary>

原有的 Token Exchange 模式继续保留兼容：先调用 `/v1/oauth2/token` 换取 `access_token`（7 天 TTL），再用 token 调用业务接口。**现有代码无需改造**，但新项目建议直接使用 API Key 直调。

```bash
# 方式 A（推荐）：API Key 作为 Bearer 直接换 token
curl -X POST https://api-m.novada.com/v1/oauth2/token \
  -H "Authorization: Bearer YOUR_API_KEY"

# 方式 B（兼容）：老的 Basic Auth (username:api_key) 仍可用
curl -X POST https://api-m.novada.com/v1/oauth2/token \
  -u "your_username:your_api_key"
```

</details>

{% hint style="info" %}
凭证管理、入参兼容矩阵、常见问题等完整说明见 [Authentication ↗](/broken/pages/7e5c09c2fe85b520c91506c8e8af012dd5b48e87)。
{% endhint %}
