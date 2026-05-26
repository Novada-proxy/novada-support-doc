---
hidden: true
---

# 网页解锁器

```
title: 默认模块
language_tabs:
  - shell: Shell
  - http: HTTP
  - javascript: JavaScript
  - ruby: Ruby
  - python: Python
  - php: PHP
  - java: Java
  - go: Go
toc_footers: []
includes: []
search: true
code_clipboard: true
highlight_theme: darkula
headingLevel: 2
generator: "@tarslib/widdershins v4.0.30"

```

## 默认模块

Base URLs:

## Authentication

* HTTP Authentication, scheme: bearer

## 抓取套餐/网页解锁器

### POST 网页解锁器

POST /request

接口地址：[https://webunlocker.novada.com](https://webunlocker.novada.com/), token的值是用户对应的api\_key

> Body 请求参数

```
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
​
```

#### 请求参数

| 名称                  | 位置   | 类型      | 必选 | 说明                                                                                                        |
| ------------------- | ---- | ------- | -- | --------------------------------------------------------------------------------------------------------- |
| body                | body | object  | 是  | none                                                                                                      |
| » target\_url       | body | string  | 是  | 目标地址                                                                                                      |
| » response\_format  | body | string  | 是  | 爬取结果输出格式，仅支持html和png，以英文逗号分割                                                                              |
| » js\_render        | body | boolean | 否  | JS渲染，true开启，false不开启。建议开启，实现抓取动态渲染、异步加载及复杂交互的内容                                                           |
| » headers           | body | string  | 否  | 自定义的headers头使用它来访问网站                                                                                      |
| » cookies           | body | string  | 否  | 自定义的 Cookie 使用它来访问网站                                                                                      |
| » country           | body | string  | 否  | 爬取时的代理国家/地区                                                                                               |
| » wait\_ms          | body | integer | 否  | 页面最大等待时间（毫秒），最大值100000毫秒                                                                                  |
| » wait\_selector    | body | string  | 否  | 等待 CSS 选择器在 DOM 中加载，若同时使用 wait\_selector和 wait\_ms，以 wait\_selector 优先（覆盖固定时间）。指定元素最长等待 30 秒，超时后自动返回网站内容。 |
| » follow\_redirects | body | string  | 否  | 当用户访问已失效的旧url时，重定向至新的url中                                                                                 |
| » block\_resources  | body | string  | 否  | 是否阻止加载图片、jc、视频等非必要资源，提升抓取速度                                                                               |
| » clear             | body | string  | 否  | 抓取结果中清理 JS、CSS不需要内容                                                                                       |
| » auto\_runs        | body | integer | 否  | 由代理失败产生的错误，可自主设置重试次数自动重试，最大重试次数为10，默认为2次                                                                  |

> 返回示例

> 200 Response

```
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

```
{}
```

#### 返回结果

| 状态码 | 状态码含义                                                          | 说明   | 数据模型   |
| --- | -------------------------------------------------------------- | ---- | ------ |
| 200 | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)        | none | Inline |
| 404 | [Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4) | none | Inline |

#### 返回数据结构

## 数据模型

<br>
