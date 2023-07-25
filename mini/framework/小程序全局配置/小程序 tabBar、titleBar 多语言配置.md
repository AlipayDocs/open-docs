# 简介

使用 tabBar、titleBar 多语言配置后，小程序会根据当前支付宝的语言来读取显示该语言配置。

多语言 tabBar、titleBar 配置如下：

1. 语言配置统一放到小程序根目录（对应 mini.project.json 中的 miniProgramRoot 配置）下的 locale 目录下。
2. 每个语言一个目录，如 zh-Hans（简体中文）、zh-HK （繁体中文香港）。
3. 在每个语言目录下，通过添加 app.json 配置，配置该语言下的 titleBar 与 tabBar。

**注意：**

- 目前仅支持 zh-Hans（简体中文）、zh-Hant（繁体中文台湾）、zh-HK（繁体中文香港）、en（英文）四种语言。
- IDE 中请使用 **真机调试** 查看配置效果。

文件目录结构示例如下：

![](http://mdn.alipayobjects.com/afts/img/A*z9X-S4YOFfMAAAAAAAAAAAAAAa8wAA/original?bz=openpt_doc&t=M4xk7mU9kmNlh19urXD5KgAAAABkMK8AAAAA#align=left&display=inline&height=614&margin=%5Bobject%20Object%5D&originHeight=614&originWidth=696&status=done&style=none&width=696)

# tabBar 真机效果

![](http://mdn.alipayobjects.com/afts/img/A*EN7qS5fNwlUAAAAAAAAAAAAAAa8wAA/original?bz=openpt_doc&t=EXyCvJ5SiOGibXswiQoqEAAAAABkMK8AAAAA#align=left&display=inline&height=854&margin=%5Bobject%20Object%5D&originHeight=854&originWidth=855&status=done&style=none&width=855)

# tabBar 示例代码

locale 目录中的 app.json 配置示例如下，`items` 中只需配置 `name` 属性的值即可。

```json
// locale/en/app.json
{
  "pages": {
    "pages/index/index": {
      "defaultTitle": "index"
    },
    "pages/second/second": {
      "defaultTitle": "second"
    },
    "pages/third/third": {
      "defaultTitle": "third"
    }
  },
  "window": {
    "defaultTitle": "Demo"
  },
  "tabBar": {
    "textColor": "#dddddd",
    "selectedColor": "#49a9ee",
    "backgroundColor": "#ffffff",
    "items": [
      {
        "name": "index"
      },
      {
        "name": "second"
      },
      {
        "name": "third"
      }
    ]
  }
}
```

根目录下的 app.json 配置示例如下，`items` 中不配置 `name` 属性。

```json
// app.json
{
  "pages": ["pages/index/index", "pages/second/second", "pages/third/third"],
  "window": {
    "defaultTitle": "Demo"
  },
  "tabBar": {
    "textColor": "#dddddd",
    "selectedColor": "#49a9ee",
    "backgroundColor": "#ffffff",
    "items": [
      {
        "pagePath": "pages/index/index"
      },
      {
        "pagePath": "pages/second/second"
      },
      {
        "pagePath": "pages/third/third"
      }
    ]
  }
}
```

# 属性

| **属性** | **类型** | **必填** | **描述**                             |
| -------- | -------- | -------- | ------------------------------------ |
| window   | Object   | 否       | 设置默认 title。                     |
| tabBar   | Object   | 否       | 设置多语言下的 tabBarItem 名称。     |
| pages    | Object   | 否       | 设置多语言下的每个页面对应的 title。 |
