# Table of contents

## 开始

* [概览](README.md)
* [快速开始](kai-shi/kuai-su-kai-shi.md)
* [认证](kai-shi/ren-zheng.md)

***

* [概览Old](gai-lan-old.md)
* [快速开始](kuai-su-kai-shi.md)

## APIsOld

* ```yaml
  type: builtin:openapi
  props:
    models: false
    downloadLink: false
  dependencies:
    spec:
      ref:
        kind: openapi
        spec: novada-api-cn-260411-1
  ```
* [抓取套餐](apisold/zhua-qu-tao-can/README.md)
  * ```yaml
    type: builtin:openapi
    props:
      models: false
      downloadLink: false
    dependencies:
      spec:
        ref:
          kind: openapi
          spec: capture-common-cn-260411-1
    ```
  * ```yaml
    type: builtin:openapi
    props:
      models: false
      downloadLink: false
    dependencies:
      spec:
        ref:
          kind: openapi
          spec: capture-unblocker-260411-1
    ```
  * [Scraper API](apisold/zhua-qu-tao-can/scraper-api.md)

## APISOld2

* ```yaml
  type: builtin:openapi
  props:
    models: false
    downloadLink: false
  dependencies:
    spec:
      ref:
        kind: openapi
        spec: 260527-1-cn-001
  ```
* [抓取套餐](apisold2/zhua-qu-tao-can/README.md)
  * ```yaml
    type: builtin:openapi
    props:
      models: false
      downloadLink: false
    dependencies:
      spec:
        ref:
          kind: openapi
          spec: capture-common-20260526
    ```
  * ```yaml
    type: builtin:openapi
    props:
      models: false
      downloadLink: false
    dependencies:
      spec:
        ref:
          kind: openapi
          spec: capture-unblocker-20260526
    ```
  * [Scraper API](apisold2/zhua-qu-tao-can/scraper-api.md)
* ```yaml
  type: builtin:openapi
  props:
    models: false
    downloadLink: false
  dependencies:
    spec:
      ref:
        kind: openapi
        spec: 260527-2-cn-001
  ```
* [错误码](apisold2/cuo-wu-ma.md)
* [限流](apisold2/xian-liu.md)

## 代理

* ```yaml
  type: builtin:openapi
  props:
    models: false
    downloadLink: false
  dependencies:
    spec:
      ref:
        kind: openapi
        spec: 2663-proxy-cn-1
  ```

## 数据采集

* ```yaml
  type: builtin:openapi
  props:
    models: false
    downloadLink: false
  dependencies:
    spec:
      ref:
        kind: openapi
        spec: 2663-capture-cn-3
  ```
* [Scraper API](shu-ju-cai-ji/scraper-api.md)

## 资源管理

* ```yaml
  type: builtin:openapi
  props:
    models: false
    downloadLink: false
  dependencies:
    spec:
      ref:
        kind: openapi
        spec: 2663-cn-resource-1
  ```

## 参考资料

* [错误码](can-kao-zi-liao/cuo-wu-ma.md)
* [限流](can-kao-zi-liao/xian-liu.md)
