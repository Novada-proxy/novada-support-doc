# Scraper API

### 创建任务

接口地址：https://scraper.novada.com/request

请求方式：POST

Content-Type：x-www-form-urlencoded

Authentication：Bearer YOUR\_API\_KEY

> 获取apikey的两种方式
>
> 方式1：[控制台](https://dashboard.novada.com/cn/overview/scraper/api/?id=25)
>
> 方式2：[接口获取](https://developer-api.novada.com/zh/apis/zhua-qu-tao-can/tong-yong)

#### 请求参数

| 名称                 | 类型      | 必选 | 说明                                                                                                                                                   |
| ------------------ | ------- | -- | ---------------------------------------------------------------------------------------------------------------------------------------------------- |
| scraper\_name      | string  | 是  | 抓取名称                                                                                                                                                 |
| scraper\_id        | number  | 是  | 抓取id                                                                                                                                                 |
| scraper\_params    | string  | 否  | 抓取参数，在非search场景下必填，具体参数参考[API参数说明](https://developer.novada.com/novada/zh/gao-ji-dai-li-jie-jue-fang-an/pa-chong-api/pa-chong-api-zhi-chi-zhan-dian) |
| scraper\_universal | string  | 否  | youtube视频参数                                                                                                                                          |
| scraper\_errors    | boolean | 是  | 是否返回错误                                                                                                                                               |
| file\_name         | string  | 否  | 自定义文件名称                                                                                                                                              |

> 请求示例

```bash
curl -X POST "https://scraper.novada.com/request" ^
  -H "Authorization: Bearer YOUR_API_KEY" ^
  -H "Content-Type: application/x-www-form-urlencoded" ^
  -d "scraper_name=amazon.com" ^
  -d "scraper_id=amazon_product_keywords" ^
  -d "scraper_errors=true" ^
  -d "scraper_params=[{\"keyword\":\"Coffer\",\"max_pages\":\"1\",\"min_price\":\"5\",\"max_price\":\"50\"}]"
```

> 返回示例 200 Response

```json
{
  "code": 0,
  "data": {
    "code": 200,
    "data": {
      "task_id": "330ae83bcff7479b9c97e586dbf93801"
    },
    "msg": "success"
  },
  "msg": "success",
  "timestamp": 1775099126
}
```

### 获取任务列表

接口地址：https://api-m.novada.com/v1/scraper/task\_list

请求方式：POST

Content-Type：x-www-form-urlencoded

Authentication：Bearer YOUR\_API\_KEY

> token获取方式：[快速开始](https://developer-api.novada.com/zh)

#### 请求参数

| 名称    | 类型     | 必选 | 说明          |
| ----- | ------ | -- | ----------- |
| limit | string | 是  | 每页大小，最大值100 |
| page  | string | 是  | 页码          |

> 请求示例

```bash
curl -X POST "https://api-m.novada.com/v1/scraper/task_list" ^
  -H "Authorization: Bearer YOUR_API_KEY" ^
  -H "Content-Type: application/x-www-form-urlencoded" ^
  -d "limit=10" ^
  -d "page=1"
```

> 返回示例 200 Response

```json
{
  "code": 0,
  "data": {
    "list": [
      {
        "api": "",
        "error_info": "",
        "fail_count": 1,
        "file_size": 0,
        "finish_time": 1774602108275,
        "id": 4537,
        "oss": "https://novada-scraper-1303252866.cos.na-siliconvalley.myqcloud.com/novada/youtube/2026/03/27/e1445fdb67454ca69da1164135679db7/e1445fdb67454ca69da1164135679db7",
        "scene": "",
        "start_time": 1774602050665,
        "status": 2,
        "success_count": 0,
        "success_rate": 0,
        "task_id": "e1445fdb67454ca69da1164135679db7",
        "total": 1,
        "unit_price": 0.0007,
        "unit_type": "flow",
        "used_quota": 0
      }
    ],
    "total": 73
  },
  "msg": "success",
  "timestamp": 1774663721
}
```

### 获取单个或者多个任务的运行状态

接口地址：https://api-m.novada.com/v1/scraper/task\_status

请求方式：POST

Content-Type：x-www-form-urlencoded

Authentication：Bearer YOUR\_API\_KEY

> token获取方式：[快速开始](https://developer-api.novada.com/zh)

#### 请求参数

| 名称        | 类型     | 必选 | 说明                            |
| --------- | ------ | -- | ----------------------------- |
| task\_ids | string | 是  | 任务id列表，以英文逗号分割，最多允许传入200个任务id |

> 请求示例

```bash
curl -X POST "https://api-m.novada.com/v1/scraper/task_status" ^
  -H "Authorization: Bearer YOUR_API_KEY" ^
  -H "Content-Type: application/x-www-form-urlencoded" ^
  -d "task_ids=330ae83bcff7479b9c97e586dbf93801"
```

> 返回示例 200 Response

```json
{
  "code": 0,
  "data": {
    "list": [
      {
        "status": "Ready",
        "task_id": "caaa5dcca21d4269af26b207b0508482"
      },
      {
        "status": "Failed",
        "task_id": "b6c22dabe35d421cb8c0c88ff6bc0971"
      }
    ]
  },
  "msg": "success",
  "timestamp": 1774663533
}
```

### 获取当前账号最后一个任务的状态

接口地址：https://api-m.novada.com/v1/scraper/last\_task\_status

请求方式：POST

Content-Type：x-www-form-urlencoded

Authentication：Bearer YOUR\_API\_KEY

> token获取方式：[快速开始](https://developer-api.novada.com/zh)

#### 请求参数

无需传参

> 返回示例 200 Response

```json
{
  "code": 0,
  "data": {
    "status": "Failed",
    "task_id": "e1445fdb67454ca69da1164135679db7"
  },
  "msg": "success",
  "timestamp": 1774662782
}
```

### 获取任务结果文件

接口地址：https://api-m.novada.com/v1/scraper/task\_download

请求方式：POST

Content-Type：x-www-form-urlencoded

Authentication：Bearer YOUR\_API\_KEY

> token获取方式：[快速开始](https://developer-api.novada.com/zh)

#### 请求参数

| 名称         | 类型     | 必选 | 说明                            |
| ---------- | ------ | -- | ----------------------------- |
| task\_ids  | string | 是  | 任务id列表，以英文逗号分割，最多允许传入200个任务id |
| file\_type | string | 是  | 文件类型：json，csv, xlsx           |

> 请求示例

```bash
curl -X POST "https://api-m.novada.com/v1/scraper/task_download" ^
  -H "Authorization: Bearer YOUR_API_KEY" ^
  -H "Content-Type: application/x-www-form-urlencoded" ^
  -d "task_ids=330ae83bcff7479b9c97e586dbf93801" ^
  -d "file_type=json"
```

> 返回示例 200 Response

```json
{
  "code": 0,
  "data": [
    {
      "download": "https://novada-scraper-1303252866.cos.na-siliconvalley.myqcloud.com/novada/google_shopping/2026/03/26/32ab51b7fb48480f9f4fdb6e0d797956.json",
      "task_id": "32ab51b7fb48480f9f4fdb6e0d797956"
    },
    {
      "download": "https://novada-scraper-1303252866.cos.na-siliconvalley.myqcloud.com/novada/youtube/2026/03/26/caaa5dcca21d4269af26b207b0508482.json",
      "task_id": "caaa5dcca21d4269af26b207b0508482"
    }
  ],
  "msg": "success",
  "timestamp": 1774664048
}
```
