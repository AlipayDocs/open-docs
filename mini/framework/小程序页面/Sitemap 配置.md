# 简介

小程序服务搜索功能目前已开放，开发者可以通过 `sitemap.json` 配置，或者[小程序服务收录](https://opendocs.alipay.com/b/03al9f)功能来配置其小程序页面是否允许小程序算法识别。当页面被小程序算法识别后，系统自动生成小程序服务，并在[搜索](https://opendocs.alipay.com/b/03al66)等场景上曝光，当用户的搜索关键词命中服务名称时，小程序服务可能展示在搜索结果中。

## 使用场景

目前该能力适用于小程序服务同步。当开启后，算法识别到小程序服务时，会在**服务管理** > **服务同步**中展示服务信息，商家可在列表页补齐信息提交审核，审核通过的小程序服务可在搜索侧展示。

![小程序服务同步示例图片](https://cdn.nlark.com/yuque/0/2022/png/179989/1648447526705-c61fccd1-518c-4b6b-98d7-0aabc5865aed.png)

# sitemap 配置

小程序根目录下的 `sitemap.json` 文件用于配置小程序及其页面是否允许被支付宝索引。文件内容为一个 JSON 对象，当小程序服务收录开关打开，如果没有 `sitemap.json`，则默认为所有页面都允许被索引。

## 配置原则

- 配置之间如果有冲突，则视作不被索引。以下文**配置示例**为参考。
- 匹配到的页面后续参数不影响索引结果，例如 `path/to/page?a=1` 等于 `path/to/page`。
- `*` 代表所有页面。

## 配置示例

根据不同需求，以下为 `sitemap.json` 的配置示例，请选择适合的配置方式。

| 索引情况 | 配置示例 |
| -------- | -------- |
| 全部页面默认允许被索引，特别指定 `path/to/page` 允许被索引，包括带参数。 | `{ "rules": [{ "page": "path/to/page" }] }` |
| 除了特别指定的 `path/to/page` 不被索引，其他页面全部允许被索引。 | `{ "rules": [{ "action": "disallow", "page": "path/to/page" }] }` |
| 所有页面都允许被索引。 | `{ "rules": [{ "page": "*" }] }` |
| 所有页面都不允许被索引。 | `{ "rules": [{ "action": "disallow", "page": "*" }] }` |
| 由于配置冲突，`path/to/page` 不被索引，其他页面也因冲突不被索引。 | `{ "rules": [{ "action": "allow", "page": "path/to/page" }, { "action": "disallow", "page": "path/to/page" }] }` |
| `path/to/page` 允许被索引，`path/to/page2` 不允许，其他页面因冲突不被索引。 | `{ "rules": [{ "action": "allow", "page": "path/to/page" }, { "action": "disallow", "page": "path/to/page2" }] }` |

## 属性

| 属性   | 类型     | 是否必填 | 描述                                    |
| ------ | -------- | -------- | --------------------------------------- |
| rules  | Object[] | 是       | 索引规则列表。                          |
| action | String   | 否       | 命中规则页面是否能被索引，默认值`allow`。可选值：`disallow`、`allow`。 |
| page   | String   | 是       | 页面路径。`*` 代表所有页面，不可作为通配符使用。     |
# IDE 调试

## 使用限制

- IDE 版本 1.16 及以上。
- sitemap 的索引提示默认开启。如需关闭 sitemap 的索引提示，请在小程序项目配置文件 `mini.project.json` 的 `setting` 中配置字段 `checkSiteMap` 为 `false`。
- sitemap 文件内容最大限制为 5120 个 UTF8 字符。

## 使用步骤

当在小程序项目中设置了 sitemap 的配置文件（默认为 `sitemap.json`）时，点击索引页面后，IDE 控制台会显示当前页面是否被索引的调试信息。

![](https://cdn.nlark.com/yuque/0/2022/png/179989/1648447533816-9d89a2d9-c848-4a46-bf3a-4a3b0b4ef1b8.png)
