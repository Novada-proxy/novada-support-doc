---
hidden: true
---

# 概览New

## Novada Public API

通过一致的接口管理代理、抓取与浏览器自动化资源。本参考文档涵盖鉴权、请求结构、错误处理、所有产品的字段定义与示例。

### 认证方式

本文档所有接口统一使用 **API Key** 作为 Bearer进行认证。在 HTTP 请求头中加入：

Authorization: Bearer YOUR\_API\_KEY

API Key 在 [仪表盘-账号设置-我的账户-API Key](https://dashboard.novada.com/cn/api-key/) 创建。完整说明见 Authentication ↗。

### 产品矩阵

本文档收录所有 Novada 产品的接口规格。计费按产品独立结算。

**代理产品（Proxy APIs）**

6 个套餐：动态住宅 / 移动 / 动态ISP / 动态数据中心 / 静态ISP / 独享数据中心。提供流量查询、IP 资源管理、可用国家/州/城市/运营商字典。

**网页解锁器（Web Unblocker）**

`POST /request` 单接口。指定 `target_url` 与 `response_format`（HTML / PNG），返回页面内容；支持 JS 渲染、自定义 headers / cookies、按国家出口。

**爬虫API（Scraper API）**

`POST /request` 创建任务，支持**同步**（响应直接返回结果）与**异步**（返回 `task_id`，后续查询 / 下载结果）两种模式。`scraper_name` 选平台、`scraper_id` 选场景。

**浏览器API（Browser API）**

云端无头浏览器，使用 username:password 通过 WebDriver / WSS 接入，兼容 Puppeteer / Playwright / Selenium。本文档收录 3 个 HTTP 管理接口（流量与字典）。

### 请求基本结构

主接入域名拆分（`api-m` / `scraper` / `webunlocker`）、协议支持范围、默认 Content-Type、版本前缀策略、统一响应包络字段（`code` / `data` / `msg` / `timestamp`）、错误响应 4 字段结构

| 主接入域名           | <p><code>api-m.novada.com</code>（绝大多数管理接口）<br><code>scraper.novada.com</code>（Scraper API 创建任务）<br><code>webunlocker.novada.com</code>（网页解锁器）</p> |
| --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| 协议              | HTTPS（HTTP/1.1 与 HTTP/2 均支持）                                                                                                                      |
| 默认 Content-Type | `application/json`（部分接口为 `application/x-www-form-urlencoded`，详见各接口页）                                                                              |
| 字符编码            | UTF-8                                                                                                                                             |
| 版本前缀            | `/v1/`                                                                                                                                            |

### 响应结构

所有 API Key 类接口返回统一响应包络：

{ "code": 200, "data": {}, "msg": "OK", "timestamp": 1779261338036 }

详见 通用响应包络 ↗。错误响应使用 4 字段结构 `{ code,data, msg,` timestamp`}`，详见 错误码 ↗。
