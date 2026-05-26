---
hidden: true
---

# 网页解锁器

### POST 网页解锁器

接口地址：https://webunlocker.novada.com

请求方式：POST

Content-Type：x-www-form-urlencoded

Authentication：Bearer YOUR\_API\_KEY

> Body 请求参数

```yaml
target_url: https://www.google.com
response_format: html
js_render: "true"
headers: ""
cookies: ""
country: us
wait_ms: 5000
wait_selector: ""
follow_redirects: ""
block_resources: ""
clear: ""
auto_runs: 0

```

#### 请求参数

<table><thead><tr><th width="198">名称</th><th width="129">类型</th><th width="97">必选</th><th>说明</th></tr></thead><tbody><tr><td>body</td><td>object</td><td>是</td><td>none</td></tr><tr><td>target_url</td><td>string</td><td>是</td><td>目标地址</td></tr><tr><td>response_format</td><td>string</td><td>是</td><td>爬取结果输出格式，仅支持html和png，以英文逗号分割</td></tr><tr><td>js_render</td><td>boolean</td><td>否</td><td>JS渲染，true开启，false不开启。建议开启，实现抓取动态渲染、异步加载及复杂交互的内容</td></tr><tr><td>headers</td><td>string</td><td>否</td><td>自定义的headers头使用它来访问网站</td></tr><tr><td>cookies</td><td>string</td><td>否</td><td>自定义的 Cookie 使用它来访问网站</td></tr><tr><td>country</td><td>string</td><td>否</td><td>爬取时的代理国家/地区</td></tr><tr><td>wait_ms</td><td>integer</td><td>否</td><td>页面最大等待时间（毫秒），最大值100000毫秒</td></tr><tr><td>wait_selector</td><td>string</td><td>否</td><td>等待 CSS 选择器在 DOM 中加载，若同时使用 wait_selector和 wait_ms，以 wait_selector 优先（覆盖固定时间）。指定元素最长等待 30 秒，超时后自动返回网站内容。</td></tr><tr><td>follow_redirects</td><td>string</td><td>否</td><td>当用户访问已失效的旧url时，重定向至新的url中</td></tr><tr><td>block_resources</td><td>string</td><td>否</td><td>是否阻止加载图片、jc、视频等非必要资源，提升抓取速度</td></tr><tr><td>clear</td><td>string</td><td>否</td><td>抓取结果中清理 JS、CSS不需要内容</td></tr><tr><td>auto_runs</td><td>integer</td><td>否</td><td>由代理失败产生的错误，可自主设置重试次数自动重试，最大重试次数为10，默认为2次</td></tr></tbody></table>

> 返回示例

> 200 Response

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

> 404 Response

```json
{}
```

#### 返回结果

| 状态码 | 状态码含义                                                          | 说明   | 数据模型   |
| --- | -------------------------------------------------------------- | ---- | ------ |
| 200 | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)        | none | Inline |
| 404 | [Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4) | none | Inline |

#### 返回数据结构

## 数据模型
