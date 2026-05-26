# 网页解锁器 | 简体中文 | Novada

`POST /request`

接口地址：https://webunlocker.novada.com，token的值是用户对应的api\_key

## Authorization

bearer

bearer

**Authorization** `string` Required

Bearer authentication header of the form `Bearer <token>`.

## Body

`application/x-www-form-urlencoded`

`application/x-www-form-urlencoded`

| 参数                 | 类型      | 必填       | 说明                                                                                                        | 示例                       |
| ------------------ | ------- | -------- | --------------------------------------------------------------------------------------------------------- | ------------------------ |
| `target_url`       | string  | Required | 目标地址                                                                                                      | `https://www.google.com` |
| `response_format`  | string  | Required | 爬取结果输出格式，仅支持html和png，以英文逗号分割                                                                              | `html`                   |
| `js_render`        | boolean | Optional | JS渲染，true开启，false不开启。建议开启，实现抓取动态渲染、异步加载及复杂交互的内容                                                           | `true`                   |
| `headers`          | string  | Optional | 自定义的headers头使用它来访问网站                                                                                      |                          |
| `cookies`          | string  | Optional | 自定义的 Cookie 使用它来访问网站                                                                                      |                          |
| `country`          | string  | Optional | 爬取时的代理国家/地区                                                                                               | `us`                     |
| `wait_ms`          | integer | Optional | 页面最大等待时间（毫秒），最大值100000毫秒                                                                                  | `5000`                   |
| `wait_selector`    | string  | Optional | 等待 CSS 选择器在 DOM 中加载，若同时使用 wait\_selector和 wait\_ms，以 wait\_selector 优先（覆盖固定时间）。指定元素最长等待 30 秒，超时后自动返回网站内容。 |                          |
| `follow_redirects` | string  | Optional | 当用户访问已失效的旧url时，重定向至新的url中                                                                                 |                          |
| `block_resources`  | string  | Optional | 是否阻止加载图片、jc、视频等非必要资源，提升抓取速度                                                                               |                          |
| `clear`            | string  | Optional | 抓取结果中清理 JS、CSS不需要内容                                                                                       |                          |
| `auto_runs`        | integer | Optional | 由代理失败产生的错误，可自主设置重试次数自动重试，最大重试次数为10，默认为2次                                                                  | `0`                      |

## Responses

`200` Success

`application/json`

`object` Optional

`404` Error

`application/json`

## HTTP

```http
POST /request HTTP/1.1
Authorization: Bearer YOUR_SECRET_TOKEN
Content-Type: application/x-www-form-urlencoded
Accept: */*
Content-Length: 226

"target_url='https://www.google.com'&response_format='html'&js_render='true'&headers=''&cookies=''&country='us'&wait_ms=5000&wait_selector=''&follow_redirects=''&block_resources=''&clear=''&auto_runs=0"
```

## 200 Success

```json
{
  "code": 0,
  "data": {
    "html": "{\"status\":\"success\",\"country\":\"United States\",\"countryCode\":\"US\",\"region\":\"NY\",\"regionName\":\"New York\",\"city\":\"Buffalo\",\"zip\":\"14205\",\"lat\":42.8864,\"lon\":-78.8784,\"timezone\":\"America/New_York\",\"isp\":\"PacketHub S.A.\",\"org\":\"Packethub S.A\",\"as\":\"AS141039 PacketHub S.A.\",\"query\":\"193.43.135.46\"}",
    "use_balance": 0.0012
  },
  "msg": "成功",
  "timestamp": 1774408181
}
```
