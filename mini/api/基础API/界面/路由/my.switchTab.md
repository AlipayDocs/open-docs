# 简介
**my.switchTab** 是跳转到指定标签页（tabbar）页面，并关闭其他所有非标签页页面的 API。

如果小程序是一个多标签（tab）应用，即客户端窗口的底部栏可以切换页面，那么可以通过标签页配置项指定标签栏的表现形式，以及标签切换时显示的对应页面。

通过页面跳转（[my.navigateTo](https://opendocs.alipay.com/mini/api/zwi8gx)）或者页面重定向（[my.redirectTo](https://opendocs.alipay.com/mini/api/fh18ky)）所到达的页面，即使是定义在标签页配置中的页面，也不会显示底部的标签栏。标签页的第一个页面必须是首页。

相关问题可查看 [路由FAQ](https://opendocs.alipay.com/mini/api/fu8l65) 。

## 使用限制
此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验

![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/e88923c5934173d172f53342d823d838.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=none&width=127)

# 接口调用

## Herbox

[小程序在线](https://herbox-embed.alipay.com/s/doc-api-navigator?theme=light&previewZoom=75&chInfo=openhome-doc) 

## 示例代码

### .json 示例代码
tabBar item 配置示例：
```json
{
  "tabBar": {
    "items": [{
      "pagePath": "page/home/index",
      "name": "首页"
    },{
      "pagePath": "page/user/index",
      "name": "用户"
    }]
  }
}
```
tabBar 配置示例：
```json
// tabBar 示例配置
{
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

### .js 示例代码

```javascript
//.js
my.switchTab({
  url: 'page/home/index'
})
```

## 入参
Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| url | String | 是 | 跳转的标签页的路径（需在 app.json 的 tabbar 字段定义的页面）。<br />**注意**：路径后不能带参数。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

## 配置

### tabBar 配置
| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| textColor | HexColor | 否 | 文字颜色。 |
| selectedColor | HexColor | 否 | 选中文字颜色。 |
| backgroundColor | HexColor | 否 | 背景色。 |
| items | Array | 是 | 每个标签（tab）配置。 |

### item 配置
| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| pagePath | String | 是 | 设置页面路径。 |
| name | String | 是 | 名称。 |
| icon | String | 否 | 普通图标路径。 |
| activeIcon | String | 否 | 高亮图标路径。 |
