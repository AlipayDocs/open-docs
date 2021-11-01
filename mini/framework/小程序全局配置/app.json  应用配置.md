`app.json` 用于对小程序进行全局配置，设置页面文件的路径、窗口表现、多 tab、分包、插件等。
以下是一个基本配置示例：
```json
{
  "pages": [
    "pages/index/index",
    "pages/logs/logs"
  ],
  "window": {
    "defaultTitle": "Demo"
  }
}
```
完整配置项如下：

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| pages | Array | 是 | 设置页面路径 |
| window | Object | 否 | 设置默认页面的窗口表现 |
| tabBar | Object | 否 | 设置底部 tabbar 的表现 |
| subPackages | Object[] | 否 | 分包结构描述 |
| subPackageBuildType | String | 否 | 分包打包策略 |
| preloadRule | Object | 否 | 分包预加载规则 |
| plugins | Object | 否 | 静态插件配置规则 |
| useDynamicPlugins | Boolean | 否 | 动态插件配置规则 |
| lazyCodeLoading |  | 否 | 是否开启代码按需执行 |


## pages
`app.json` 中的 `pages` 为数组属性，数组中每一项都是字符串，用于指定小程序的页面。在小程序中新增或删除页面，都需要对 `pages` 数组进行修改。
`pages` 数组的每一项代表对应页面的路径信息，其中，第一项代表小程序的首页。
页面路径不需要写任何后缀，框架会自动去加载同名的 `.json`、`.js`、`.axml`、`.acss` 文件。举例来说，如果开发目录为：

```javascript
├── pages
│   ├──index
│   │    ├── index.json
│   │    ├── index.js
│   │    ├── index.axml
│   │    └── index.acss
│   ├──logs
│   │    ├── logs.json
│   │    ├── logs.js
│   │    └── logs.axml
├── app.json
├── app.js
└── app.acss
```
`app.json` 中应当如下配置：
```json
{
  "pages":[
    "pages/index/index",
    "pages/logs/logs"
  ]
}
```

## window
`window` 用于设置小程序的状态栏、导航条、标题、窗口背景色等。
示例代码：
```json
{
  "window":{
    "defaultTitle": "支付宝接口功能演示"
  }
}
```
| **属性** | **类型** | **是否必填** | **描述** | **最低版本** |
| --- | --- | --- | --- | --- |
| defaultTitle | String | 否 | 页面默认标题。 | - |
| pullRefresh | Boolean | 否 | 是否允许下拉刷新，默认 `true`。<br /> **说明：** <br /> 1.下拉刷新生效的前提是 allowsBounceVertical 值为 YES。<br /> 2.window 全局配置后全局生效，但是如果单个页面配置了该参数，以页面的配置为准。| - |
| allowsBounceVertical | String | 否 | 是否允许向下拉拽。默认 `YES`, 支持 `YES` / `NO` | - |
| transparentTitle | String | 否 | 导航栏透明设置。默认 `none`，支持 `always` 一直透明 / `auto` 滑动自适应 / `none` 不透明。 | - |
| titlePenetrate | String | 否 | 是否允许导航栏点击穿透。默认 `NO`，支持 `YES` / `NO`。 | - |
| showTitleLoading | String | 否 | 是否进入时显示导航栏的 loading。默认 `NO`，支持 `YES` / `NO`。 | - |
| titleImage | String | 否 | 导航栏图片地址。 | - |
| titleBarColor | HexColor | 否 | 导航栏背景色。例：白色 "#FFFFFF"。 | - |
| backgroundColor | HexColor | 否 | 页面的背景色。例：白色 "#FFFFFF"。 | - |
| backgroundImageColor | HexColor | 否 | 下拉露出显示背景图的底色。例：白色 "#FFFFFF"。 | - |
| backgroundImageUrl | String | 否 | 下拉露出显示背景图的链接。 | - |
| gestureBack | String | 否 | 仅支持 iOS，是否支持手势返回。默认 `YES`，支持 `YES` / `NO`。 | - |
| enableScrollBar | String | 否 | 仅支持 Android，是否显示 `WebView` 滚动条。默认 `YES`，支持 `YES` / `NO`。 | - |
| onReachBottomDistance | Number | 否 | 页面上拉触底时触发时距离页面底部的距离，单位为 `px`，详情请参见 [页面事件处理函数](/mini/framework/page-detail#%E9%A1%B5%E9%9D%A2%E4%BA%8B%E4%BB%B6%E5%A4%84%E7%90%86%E5%87%BD%E6%95%B0)。 | [1.19.0](https://opendocs.alipay.com/mini/framework/compatibility) ，目前`iOS`在`page.json`下设置无效，只能全局设置。 |
| responsive | Boolean | 否 | `rpx` 单位是否宽度自适应 ，默认true，当设置为 `false` 时，2 rpx 将恒等于 1 px，不再根据屏幕宽度进行自适应，注意，此时 750 rpx 将不再等于100% 宽度。 | [1.23.0](https://opendocs.alipay.com/mini/framework/compatibility) |


## tabBar
如果开发的小程序是一个多 tab 应用（客户端窗口的底部栏可以切换页面），那么可以通过 `tabBar` 配置项指定 tab 栏的表现，以及 tab 切换时显示的对应页面。
`tabBar` 与 `pages`、 `window` 配置同级，配置项如下：

| **属性** | **类型** | **是否必填** | **描述** |
| --- | --- | --- | --- |
| textColor | HexColor | 否 | 文字颜色 |
| selectedColor | HexColor | 否 | 选中文字颜色 |
| backgroundColor | HexColor | 否 | 背景色 |
| items | Array | 是 | 每个 tab 配置 |

每个 item 配置：

| **属性** | **类型** | **是否必填** | **描述** |
| --- | --- | --- | --- |
| pagePath | String | 是 | 设置页面路径 |
| name | String | 是 | 名称 |
| icon | String | 否 | 平常图标路径（非选中状态） |
| activeIcon | String | 否 | 高亮图标路径（选中状态） |

icon 图标推荐大小为 60×60 px 大小，系统会对传入的非推荐尺寸的图片进行非等比拉伸或缩放。
带有 `tabBar` 的 `app.json` 示例如下：

```json
{
"pages": [
    "pages/index/index",
    "pages/logs/logs"
  ],
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
代码中，开发者可通过 [my.setTabBarItem](https://opendocs.alipay.com/mini/api/zu37bk) 动态设置 `tabBar` 中指定 `item` 的内容。

## subPackages
启用 [分包加载](https://opendocs.alipay.com/mini/framework/subpackages) 时，声明项目分包结构。

## preloadRule
声明 [分包预下载](https://opendocs.alipay.com/mini/framework/subpackages#%E5%88%86%E5%8C%85%E9%A2%84%E4%B8%8B%E8%BD%BD) 的规则。

## subPackageBuildType
声明 [分包内同一模块的隔离策略](https://opendocs.alipay.com/mini/framework/subpackages#%E5%88%86%E5%8C%85%E5%86%85%E5%90%8C%E4%B8%80%E6%A8%A1%E5%9D%97%E7%9A%84%E9%9A%94%E7%A6%BB%E7%AD%96%E7%95%A5) 。

## plugins
基础库 1.22.4 及以上，支付宝客户端 10.1.85 及以上开始支持。
声明小程序需要使用的 [静态插件](https://opendocs.alipay.com/mini/plugin/plugin-usage#%E9%9D%99%E6%80%81%E5%A3%B0%E6%98%8E)。

## useDynamicPlugins
基础库 1.22.4 及以上，支付宝客户端 10.1.85 及以上开始支持。
声明小程序需要使用 [动态插件](https://opendocs.alipay.com/mini/plugin/plugin-usage#%E5%8A%A8%E6%80%81%E5%8A%A0%E8%BD%BD)。

## lazyCodeLoading
小程序应用的启动过程中，除了下载阶段以外，默认会执行所有代码（包括当前页面未使用到的所有页面、自定义组件），会对启动耗时有一定影响。
基础库 2.7.0 及以上 ，支持配置以下 lazyCodeLoading 参数，仅执行当前页面所必须的页面脚本和自定义组件脚本，其他脚本则不会被执行。
```javascript
{
  "lazyCodeLoading": "requiredComponents"
}
```
**注意：**由于开启该配置后，当前页面未使用到的代码将不会被执行，可能对某些依赖默认脚本执行先后顺序的逻辑产生影响。

## workers
使用 [Worker](https://opendocs.alipay.com/mini/api/createworker) 处理多线程任务时，设置 Worker 代码文件列表。如：
```json
"workers": [
  "workers/index.js"
]
```


