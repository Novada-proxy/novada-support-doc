# 概览\_New

## Novada Public API

通过一致的接口管理代理、抓取与浏览器自动化资源。本参考文档涵盖鉴权、请求结构、错误处理、所有产品的字段定义与示例。

***

## 认证方式

本文档所有接口统一使用 **API Key** 作为 Bearer进行认证。在 HTTP 请求头中加入：

```http
Authorization: Bearer YOUR_API_KEY
```

{% hint style="info" %}
API Key 在 [**仪表盘 - 账号设置 - 我的账户 - API Key**](https://dashboard.novada.com/cn/api-key/) 创建。完整说明见 [Authentication ↗](/broken/pages/9843913ec88038924ee8001d60b1326dd3d9d0a8)。
{% endhint %}

***

## 产品矩阵

本文档收录所有 Novada 产品的接口规格。计费按产品独立结算。

<table data-view="cards"><thead><tr><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="image">Cover image</th></tr></thead><tbody><tr><td><strong>🅟 代理产品（Proxy APIs）</strong></td><td>6 个套餐：动态住宅 / 移动 / 动态 ISP / 动态数据中心 / 静态 ISP / 独享数据中心。提供流量查询、IP 资源管理、可用国家 / 州 / 城市 / 运营商字典。</td><td><a href="/broken/pages/f565e4c8778970c9cdf647fcf5451f5edd617b43">Broken link</a></td><td></td></tr><tr><td><strong>🅤 网页解锁器（Web Unblocker）</strong></td><td><code>POST /request</code> 单接口。指定 <code>target_url</code> 与 <code>response_format</code>（HTML / PNG），返回页面内容；支持 JS 渲染、自定义 headers / cookies、按国家出口。</td><td><a href="/broken/pages/775eecc449f782ef3f5e9e6b5f550382d7555da1">Broken link</a></td><td></td></tr><tr><td><strong>🅢 爬虫 API（Scraper API）</strong></td><td><code>POST /request</code> 创建任务，支持<strong>同步</strong>（响应直接返回结果）与<strong>异步</strong>（返回 <code>task_id</code>，后续查询 / 下载结果）两种模式。<code>scraper_name</code> 选平台、<code>scraper_id</code> 选场景。</td><td><a href="../apis/zhua-qu-tao-can/scraper-api.md">scraper-api.md</a></td><td></td></tr><tr><td><strong>🅑 浏览器 API（Browser API）</strong></td><td>云端无头浏览器，使用 <code>username:password</code> 通过 WebDriver / WSS 接入，兼容 Puppeteer / Playwright / Selenium。本文档收录 3 个 HTTP 管理接口（流量与字典）。</td><td><a href="/broken/pages/ab85ec7c9c32de52bbd01f72bdd7f76eee0fb18a">Broken link</a></td><td></td></tr></tbody></table>

***

## 请求基本结构

<table><thead><tr><th width="180">项目</th><th>说明</th></tr></thead><tbody><tr><td><strong>主接入域名</strong></td><td><code>api-m.novada.com</code> · 绝大多数管理接口<br><code>scraper.novada.com</code> · Scraper API 创建任务<br><code>webunlocker.novada.com</code> · 网页解锁器</td></tr><tr><td><strong>协议</strong></td><td>HTTPS（HTTP/1.1 与 HTTP/2 均支持）</td></tr><tr><td><strong>默认 Content-Type</strong></td><td><code>application/json</code>（部分接口为 <code>application/x-www-form-urlencoded</code>，详见各接口页）</td></tr><tr><td><strong>字符编码</strong></td><td>UTF-8</td></tr><tr><td><strong>版本前缀</strong></td><td><code>/v1/</code></td></tr></tbody></table>

***

## 响应结构

所有 API Key 类接口返回**统一响应包络**：

```json
{
  "code": 200,
  "data": {},
  "msg": "OK",
  "timestamp": 1779261338036
}
```

{% hint style="info" %}
字段含义详见 [通用响应包络 ↗](/broken/pages/89b274a73c05f7f6071092c60955d0e9085537e8)，错误场景下的 `code` 取值详见 [错误码 ↗](/broken/pages/89b274a73c05f7f6071092c60955d0e9085537e8)。
{% endhint %}
