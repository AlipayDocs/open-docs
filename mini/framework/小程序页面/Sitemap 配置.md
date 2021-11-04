
# 简介
小程序服务搜索功能目前已开放，开发者可以通过 sitemap.json 配置，或者 [小程序服务收录](https://opendocs.alipay.com/mini/operation/service-included) 功能来配置其小程序页面是否允许小程序算法识别。当页面被小程序算法识别后，系统自动生成小程序服务，并在 [搜索](https://opendocs.alipay.com/mini/operation/search-service) 等场景上曝光，当用户的搜索关键词命中服务名称时，小程序服务可能展示在搜索结果中。

## 使用场景
目前该能力适用在 [小程序服务同步](https://opendocs.alipay.com/mini/operation/service-synchronization)。当开启后算法识别到小程序服务时，会在 **服务管理** > **服务同步** 中展示服务信息，商户可在列表页补齐信息提交审核，审核通过的小程序服务可在搜索侧展示。 

![|223x478](https://intranetproxy.alipay.com/skylark/lark/0/2020/png/10334/1603681765167-162909ae-3f22-4bb9-8af9-b569c879f894.png#align=left&display=inline&height=478&margin=%5Bobject%20Object%5D&originHeight=954&originWidth=445&status=done&style=none&width=223)    

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
| 1.action 不配置默认允许被索引 <br /> 2.path/to/page：被索引 <br /> 3.path/to/page?a=1 ：被索引<br /> 4.其他页面都不会被索引 |``` {"rules":[{  "page": "path/to/page" }] }``` |
| 1.path/to/page ：不被索引 <br /> 2.其他页面被索引 | ```{ "rules":[{ "action": "disallow", "page": "path/to/page" }] }``` |
| 所有页面都被索引 | ``` { "rules":[{ "page": "*" }] }``` |
| 所有页面都不被索引 | ``` { "rules":[{ "action": "disallow", "page": "*" }] }``` |
| 1.path/to/page：因为冲突不被索引 <br /> 2.其他页面因为冲突也不会被索引 | ``` { "rules":[{ "action": "allow", "page": "path/to/page" }, { "action": "disallow", "page": "path/to/page" }] }``` |
| 1.path/to/page：被索引 <br /> 2.path/to/page2：不被索引 <br /> 3.其他页面因为冲突不会被索引 | ``` { "rules":[{ "action": "allow", "page": "path/to/page" }, { "action": "disallow", "page": "path/to/page2" }] }``` |


# IDE 调试

## 使用限制

- IDE 版本 1.16 及以上。
- sitemap 的索引提示是默认开启的，如需要关闭 sitemap 的索引提示，可在小程序项目配置文件 project.config.json 的 setting 中配置字段 checkSiteMap 为 false。
- sitemap 文件内容最大为 5120 个 UTF8 字符。


## 使用步骤
当在小程序项目中设置了 sitemap 的配置文件（默认为 sitemap.json）时，点击索引页面时便可在 IDE 控制台上显示当前页面是否被索引的调试信息。
![](https://intranetproxy.alipay.com/skylark/lark/0/2020/png/236382/1604456350281-394bf8a6-71b3-4c6e-b5f3-cb2e885609db.png#align=left&display=inline&height=1041&margin=%5Bobject%20Object%5D&originHeight=1041&originWidth=1920&status=done&style=none&width=1920)
