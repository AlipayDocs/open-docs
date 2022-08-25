# 简介
小程序服务搜索功能目前已开放，开发者可以通过 sitemap.json 配置，或者 [小程序服务收录](https://opendocs.alipay.com/b/03al9f) 功能来配置其小程序页面是否允许小程序算法识别。当页面被小程序算法识别后，系统自动生成小程序服务，并在 [搜索](https://opendocs.alipay.com/b/03al66) 等场景上曝光，当用户的搜索关键词命中服务名称时，小程序服务可能展示在搜索结果中。

## 使用场景

目前该能力适用在小程序服务同步。当开启后算法识别到小程序服务时，会在 **服务管理** > **服务同步** 中展示服务信息，商家可在列表页补齐信息提交审核，审核通过的小程序服务可在搜索侧展示。 

![|223x478](https://cdn.nlark.com/yuque/0/2022/png/179989/1648447526705-c61fccd1-518c-4b6b-98d7-0aabc5865aed.png)    

# sitemap 配置

小程序根目录下的 `sitemap.json` 文件用于配置小程序及其页面是否允许被支付宝索引，文件内容为一个 JSON 对象，小程序服务收录开关打开时，如果没有 `sitemap.json` 则默认为所有页面都允许被索引。 

## 配置原则 

- 配置之间如有冲突，视作不被索引。冲突示例见下文 **配置示例**。
- 匹配页面后面的参数不影响索引结果，示例： `path/to/page?a =1`  等于 `path/to/page`。
- `*` 代表所有页面。

## 配置示例

以下分别为不同情况下 `sitemap.json` 的配置，请根据需要进行配置。

| **索引** | **配置示例** |
| --- | --- |
| <ol><li>action 不配置默认允许被索引。</li><li>path/to/page：被索引。</li><li>path/to/page?a=1 ：被索引。</li><li>其他页面都不会被索引。</li></ol> | `{"rules":[{  "page": "path/to/page" }] }` |
| <ol><li>path/to/page ：不被索引。</li><li>其他页面被索引。</li></ol> | `{ "rules":[{ "action": "disallow", "page": "path/to/page" }] }` |
| 所有页面都被索引。 | `{ "rules":[{ "page": "*" }] }` |
| 所有页面都不被索引。 | `{ "rules":[{ "action": "disallow", "page": "*" }] }` |
| <ol><li>path/to/page：因为冲突不被索引。</li><li>其他页面因为冲突也不会被索引。</li></ol> | `{ "rules":[{ "action": "allow", "page": "path/to/page" }, { "action": "disallow", "page": "path/to/page" }] }` |
| <ol><li>path/to/page：被索引。</li><li>path/to/page2：不被索引。</li><li>其他页面因为冲突不会被索引。</li></ol> | `{ "rules":[{ "action": "allow", "page": "path/to/page" }, { "action": "disallow", "page": "path/to/page2" }] }` |

## 属性
| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| rules | Object[] | 是 | 索引规则列表。 |
| action | String | 否 | 命中该规则的页面是否能被索引。<br /> **默认值**：disallow。 <br /> **可选值**：disallow、allow。 |
| page | String | 是 | 页面路径。<br /> **说明**：`*` 表示所有页面，不能作为通配符使用。 |

# IDE 调试
## 使用限制
- IDE 版本 1.16 及以上。
- sitemap 的索引提示是默认开启的，如需要关闭 sitemap 的索引提示，可在小程序项目配置文件 mini.project.json 的 setting 中配置字段 checkSiteMap 为 false。
- sitemap 文件内容最大为 5120 个 UTF8 字符。

## 使用步骤
当在小程序项目中设置了 sitemap 的配置文件（默认为 sitemap.json）时，点击索引页面时便可在 IDE 控制台上显示当前页面是否被索引的调试信息。
![](https://cdn.nlark.com/yuque/0/2022/png/179989/1648447533816-9d89a2d9-c848-4a46-bf3a-4a3b0b4ef1b8.png)
