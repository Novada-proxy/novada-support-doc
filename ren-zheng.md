# 认证

### 凭证模式

当前主路径为 **API Key 直调**。并为已使用 Token 模式的老代码**长期保留兼容**，无需改造。

{% hint style="success" %}
**✅ CURRENT — API Key 直调（推荐）**

单步直调，无需换 token，无过期问题。

```bash
curl -X POST https://api-m.novada.com/v1/wallet/balance \
  -H "Authorization: Bearer YOUR_API_KEY"
```
{% endhint %}

<details>

<summary>兼容保留：Token Exchange 模式（老用户无需改造）</summary>

先调用 `/v1/oauth2/token` 换取 `access_token`（7 天 TTL）再调业务接口。**现有代码无需改造**，但新项目建议直接使用 API Key 直调。

```bash
curl -X POST https://api-m.novada.com/v1/oauth2/token \
  -H "Authorization: Bearer YOUR_API_KEY"

# 老 Basic Auth (username:api_key) 兼容保留
```

</details>

### 如何生成新 API Key

注册账号后系统自动创建一个默认 Key。如需更多 Key（环境隔离、轮换），按以下步骤新建：

1.  **登录控制台**

    访问 [**仪表盘 - 账号设置 - 我的账户 - API Key**](https://dashboard.novada.com/cn/api-key/)。
2.  **点击「新建 API Key」**

    列表页右上角，单账号最多 10 个 Key。
3.  **配置 Key 信息**

    设置名称（如 `prod-server`）与有效期（最长 5 年，可设永不过期）。
4.  **复制并保存**

    保存到密码管理器或 secret 存储（避免明文进代码仓库）。Key 可在仪表盘随时查看与复制。

### API Key 管理

| 项目      | 说明                                                                                                                                                                                                                                                                |
| ------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 入口      | [仪表盘 - 账号设置 - 我的账户 - API Key](https://dashboard.novada.com/cn/api-key/)                                                                                                                                                                                           |
| 数量      | 单账号最多 **10 个** API Key，可独立启停。                                                                                                                                                                                                                                     |
| 有效期     | 默认最长 5 年，**可设永不过期**。仪表盘内可随时修改。                                                                                                                                                                                                                                    |
| 启用 / 禁用 | 立即生效。禁用后调用立刻返回 `401 api_key_disabled`。                                                                                                                                                                                                                            |
| 套餐解耦    | 套餐到期返回 `402 product_not_subscribed`，**Key 本身仍有效**，续费后即可恢复。                                                                                                                                                                                                        |
| 覆盖范围    | <p>一 Key 覆盖：开放接口、Scraper API、Web Unblocker 全部接口（均为 HTTP/HTTPS，统一通过 <code>Authorization: Bearer YOUR_API_KEY</code> 传递）。<br>⚠️ <strong>Browser API 实际浏览器接入</strong>（WebDriver / WSS）使用 <code>username:password</code> 凭证，不在 API Key 覆盖范围内（详见 Browser API 产品页）。</p> |

### 常见问题

<details>

<summary>API Key 丢失或泄露怎么办？</summary>

API Key 与账号密码同等敏感。一旦怀疑泄露，请立即在 [**仪表盘 - 账号设置 - 我的账户 - API Key**](https://dashboard.novada.com/cn/api-key/) 删除旧 Key 并新建一个，再把生产环境的引用替换为新 Key。

删除后旧 Key 的所有调用会立刻返回 `apikey invalid`。建议先创建新 Key、灰度切换完成后再删除旧 Key。

</details>

<details>

<summary>能否在仪表盘查看已有 API Key 的明文？</summary>

可以。Novada 控制台允许在 API Key 列表中随时查看与复制已创建的 Key，不会因为关闭页面而丢失。即便如此，也建议在生成时立即保存到密码管理器或 secret 存储，便于在多人 / 多环境下集中管理。

</details>

<details>

<summary>能不能"刷新"已有的 API Key（保留 ID 仅换值）？</summary>

Novada 当前不支持"原位刷新"。轮换流程为：**新建 → 替换引用 → 删除旧 Key**。新旧 Key 可以在轮换期内短期并存，便于灰度切换。

</details>

<details>

<summary>单账号能创建多少个 API Key？</summary>

单账号最多 **10 个** API Key，可独立启停。常见用法是为 dev / staging / prod 各创建一个，或为不同业务线 / 不同应用各分配一个，便于精细化追踪用量与定位泄露源。

</details>

<details>

<summary>API Key 有权限分级吗？</summary>

当前所有 API Key 等效全权限，可访问账号下所有产品的所有接口。Key 之间的差异仅在于：名称、有效期、启用状态、用量统计。

未来计划支持权限粒度分级（按产品 / 按操作类型），届时新建 Key 时可勾选权限范围。

</details>

<details>

<summary>套餐到期了，API Key 还能用吗？</summary>

API Key 与套餐解耦。套餐到期时，**API Key 本身仍然有效**。续费后立即恢复，无需重新生成 Key、无需修改应用代码。

</details>

<details>

<summary>所有产品共用一个 API Key 吗？</summary>

API Key 类产品（开放接口、Scraper API、Web Unblocker）**一 Key 通吃**，统一在 Header 中带 `Authorization: Bearer YOUR_API_KEY` 即可。

⚠️ **Browser API 实际浏览器接入**（WebDriver / WSS 端点）和**代理服务运行时接入**（拨号）使用 `username:password` 凭证，不属于 API Key 体系。Browser API 在 `api-m.novada.com` 上的 3 个 HTTP 流量管理接口仍走 API Key。

</details>

### 安全建议

| 项目   | 建议                                                                      |
| ---- | ----------------------------------------------------------------------- |
| 轮换   | 建议每 90 天轮换一次生产 Key。新旧 Key 可短期并存。                                        |
| 分离   | 为 dev / staging / prod 创建独立 Key；不要把生产 Key 用于本地开发。                       |
| 入库   | 不要提交到 Git；使用 `.env` + secret 管理（Vault / Doppler / AWS Secrets Manager）。 |
| 最小权限 | 未来 Key 将支持权限粒度分级，当前所有 Key 等效全权限。                                        |
