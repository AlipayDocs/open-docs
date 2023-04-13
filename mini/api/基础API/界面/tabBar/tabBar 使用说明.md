多 tab 小程序（小程序的底部栏可以切换页面）可以通过 `tabBar` 配置项指定 tab 栏的表现，以及 tab 切换时显示的对应页面。

**注意**：

- 通过页面跳转（`my.navigateTo`）或者页面重定向（`my.redirectTo`）所到达的页面，即使它是定义在 tabBar 配置中的页面，也不会显示底部的 tab 栏。
- `tabBar` 的 `icon` 暂不支持 GIF 动画。

# tabBar 配置

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| textColor | HexColor | 否 | 文字颜色。 |
| selectedColor | HexColor | 否 | 选中文字颜色。 |
| backgroundColor | HexColor | 否 | 背景色。 |
| items | Array | 是 | 每个 tab 的配置。单个 item 的配置属性见下表。 |

# item 配置

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| pagePath | String | 是 | 设置页面路径。 |
| name | String | 是 | 名称。 |
| icon | String | 否 | 平常图标路径。<br />icon 推荐图片尺寸为 60\*60px ，系统会对任意传入的图片非等比拉伸或缩放。 |
| activeIcon | String | 否 | 高亮图标路径。 |

# 示例代码

带有 tabBar 的 app.json 示例如下：

```json
{
  "pages": ["pages/index/index", "pages/logs/index"],
  "window": {
    "defaultTitle": "Demo"
  },
  "tabBar": {
    "textColor": "#dddddd",
    "selectedColor": "#49a9ee",
    "backgroundColor": "#ffffff",
    "items": [
      {
        "pagePath": "pages/index/index",
        "name": "首页"
      },
      {
        "pagePath": "pages/logs/logs",
        "name": "日志"
      }
    ]
  }
}
```

代码中，开发者可以通过 [my.setTabBarItem](https://opendocs.alipay.com/mini/api/zu37bk) 动态设置 tabBar 中指定 item 的内容。
