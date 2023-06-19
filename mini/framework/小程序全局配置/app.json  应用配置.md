[openvideo-应用配置](https://gw.alipayobjects.com/mdn/rms_aefee5/afts/file/A*rfoRSI3JCrMAAAAAAAAAAAAAARQnAQ) `app.json` 用于对小程序进行全局配置，设置页面文件的路径、窗口表现、多 tab、分包、插件等。

以下是一个基本配置示例：

```json
{
  "pages": ["pages/index/index", "pages/logs/logs"],
  "window": {
    "defaultTitle": "Demo"
  }
}
```

完整配置项如下：

| **属性**            | **类型** | **必填** | **描述**                       |
| ------------------- | -------- | -------- | ------------------------------ |
| entryPagePath       | String   | 否       | 小程序默认启动首页。           |
| pages               | Array    | 是       | 设置页面路径。                 |
| window              | Object   | 否       | 设置默认页面的窗口表现。       |
| tabBar              | Object   | 否       | 设置底部 tabbar 的表现。       |
| subPackages         | Object[] | 否       | 分包结构描述。                 |
| preloadRule         | Object   | 否       | 分包预加载规则。               |
| plugins             | Object   | 否       | 静态插件配置规则。             |
| useDynamicPlugins   | Boolean  | 否       | 动态插件配置规则。             |
| usingComponents     | Array    | 否       | 设置全局自定义组件声明。       |
| lazyCodeLoading     | String   | 否       | 是否开启代码按需执行。         |
| permission          | Object   | 否       | 小程序接口权限相关配置。       |
| behavior            | Object   | 否       | 修改小程序运行行为的相关设置。 |
| workers             | Array    | 否       | 设置 Worker 代码文件列表。 |

# entryPagePath

指定小程序的默认启动路径（首页）。如果不填，将默认为 pages 列表的第一项。不支持带页面路径参数。

**注意**：此特性从基础库 [2.7.20](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2)，[IDE 3.1.2](https://opendocs.alipay.com/mini/ide/download) 开始支持。若强依赖此特性，建议设置最低基础库版本号为 2.7.20。否则，在低版本的基础库，会因为无法识别正确的首页而导致渲染出 **返回首页** 图标。

# pages

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
  "pages": ["pages/index/index", "pages/logs/logs"]
}
```

# usingComponents

在 app.json 中声明的自定义组件将会认为成全局自定义组件，在小程序各页面或自定义组件中可以直接使用无需额外声明。

```json
{
  "usingComponents": {
    "com1": "/components/com1/index",
    "com2": "./components/com2/index"
  }
}
```

**注意**：[IDE3.1.2](https://opendocs.alipay.com/mini/ide/download) 及以上开始支持。该功能声明的组件将要被所有页面和组件依赖，可能会影响性能，且会占用主包大小，建议开启 app.lazyCodeLoading。

# window

`window` 用于设置小程序的状态栏、导航条、标题、窗口背景色等。示例代码：

```json
{
  "window": {
    "defaultTitle": "支付宝接口功能演示"
  }
}
```

| **属性** | **类型** | **必填** | **描述** | **最低版本** |
| --- | --- | --- | --- | --- |
| allowsBounceVertical | String | 否 | 是否允许向下拉拽。默认 `YES`, 支持 `YES` / `NO` | - |
| backgroundColor | HexColor | 否 | 页面的背景色。例：白色 "#FFFFFF"。 | - |
| backgroundImageColor | HexColor | 否 | 下拉露出显示背景图的底色。例：白色 "#FFFFFF"。**仅安卓下有效，iOS 下页面背景图底色会使用 backgroundColor 的值** | - |
| backgroundImageUrl | String | 否 | 下拉露出显示背景图的链接。 | - |
| defaultTitle | String | 否 | 页面默认标题。 | - |
| enableScrollBar | String | 否 | 仅支持 Android，是否显示 `WebView` 滚动条。默认 `YES`，支持 `YES` / `NO`。 | - |
| gestureBack | String | 否 | 仅支持 iOS，是否支持手势返回。默认 `YES`，支持 `YES` / `NO`。 | - |
| onReachBottomDistance | Number | 否 | 页面上拉触底时触发时距离页面底部的距离，单位为 `px`，详情可查看 [页面事件处理函数](https://opendocs.alipay.com/mini/framework/page-detail#%E9%A1%B5%E9%9D%A2%E4%BA%8B%E4%BB%B6%E5%A4%84%E7%90%86%E5%87%BD%E6%95%B0)。 | [1.19.0](https://opendocs.alipay.com/mini/framework/compatibility) ，目前`iOS`在`page.json`下设置无效，只能全局设置。 |
| pullRefresh | Boolean | 否 | 是否允许下拉刷新，默认 `false`。<br /> **说明：** <br /> 1.下拉刷新生效的前提是 allowsBounceVertical 值为 YES。<br /> 2.window 全局配置后全局生效，但是如果单个页面配置了该参数，以页面的配置为准。 | - |
| responsive | Boolean | 否 | `rpx` 单位是否宽度自适应 ，默认 true，当设置为 `false` 时，2 rpx 将恒等于 1 px，不再根据屏幕宽度进行自适应，注意，此时 750 rpx 将不再等于 100% 宽度。 | [1.23.0](https://opendocs.alipay.com/mini/framework/compatibility) |
| showTitleLoading | String | 否 | 是否进入时显示导航栏的 loading。默认 `NO`，支持 `YES` / `NO`。 | - |
| transparentTitle | String | 否 | 导航栏透明设置。默认 `none`，支持 `always` 一直透明 / `auto` 滑动自适应 / `none` 不透明。 | - |
| titlePenetrate | String | 否 | 是否允许导航栏点击穿透。默认 `NO`，支持 `YES` / `NO`。 | - |
| titleImage | String | 否 | 导航栏图片地址。 | - |
| titleBarColor | HexColor | 否 | 导航栏背景色。例：白色 "#FFFFFF"。 | - |

# tabBar

如果开发的小程序是一个多 tab 应用（客户端窗口的底部栏可以切换页面），那么可以通过 `tabBar` 配置项指定 tab 栏的表现，以及 tab 切换时显示的对应页面。 `tabBar` 与 `pages`、 `window` 配置同级，配置项如下：

| **属性**        | **类型** | **必填** | **描述**        |
| --------------- | -------- | -------- | --------------- |
| textColor       | HexColor | 否       | 文字颜色。      |
| selectedColor   | HexColor | 否       | 选中文字颜色。  |
| backgroundColor | HexColor | 否       | 背景色。        |
| items           | Array    | 是       | 每个 tab 配置。 |

每个 item 配置：

| **属性**   | **类型** | **必填** | **描述**                     |
| ---------- | -------- | -------- | ---------------------------- |
| pagePath   | String   | 是       | 设置页面路径。               |
| name       | String   | 是       | 名称。                       |
| icon       | String   | 否       | 平常图标路径（非选中状态）。 |
| activeIcon | String   | 否       | 高亮图标路径（选中状态）。   |

icon 图标推荐大小为 81px \* 81px，系统会对传入的非推荐尺寸的图片进行非等比拉伸或缩放。带有 `tabBar` 的 `app.json` 示例如下：

```json
{
  "pages": ["pages/index/index", "pages/logs/logs"],
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

# subPackages

启用 [分包加载](https://opendocs.alipay.com/mini/framework/subpackages) 时，声明项目分包结构。

# preloadRule

声明 [分包预下载](https://opendocs.alipay.com/mini/framework/subpackages#%E5%88%86%E5%8C%85%E9%A2%84%E4%B8%8B%E8%BD%BD) 的规则。

# plugins

基础库 1.22.4 及以上，支付宝客户端 10.1.85 及以上开始支持。声明小程序需要使用的 [静态插件](https://opendocs.alipay.com/mini/plugin/plugin-usage#%E9%9D%99%E6%80%81%E5%A3%B0%E6%98%8E)。

# useDynamicPlugins

基础库 1.22.4 及以上，支付宝客户端 10.1.85 及以上开始支持。声明小程序需要使用 [动态插件](https://opendocs.alipay.com/mini/plugin/plugin-usage#%E5%8A%A8%E6%80%81%E5%8A%A0%E8%BD%BD)。

# lazyCodeLoading

小程序应用的启动过程中，除了下载阶段以外，默认会执行所有代码（包括当前页面未使用到的所有页面、自定义组件），会对启动耗时有一定影响。基础库 2.7.0 及以上 ，支持配置以下 lazyCodeLoading 参数，仅执行当前页面所必须的页面脚本和自定义组件脚本，其他脚本则不会被执行。

```javascript
{
  "lazyCodeLoading": "requiredComponents"
}
```

**注意：** 由于开启该配置后，当前页面未使用到的代码将不会被执行，可能对某些依赖默认脚本执行先后顺序的逻辑产生影响。

# workers

使用 [Worker](https://opendocs.alipay.com/mini/api/createworker) 处理多线程任务时，设置 Worker 代码文件列表。如：

```json
"workers": [
  "workers/index.js"
]
```

# permission

小程序接口权限相关设置。字段类型为 Object，结构为：

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| scope.album | PermissionObject | 否 | 相册（访问）相关权限声明，相关 API：[my.chooseImage](https://opendocs.alipay.com/mini/api/media/image/my.chooseimage)、[my.chooseVideo](https://opendocs.alipay.com/mini/api/media/video/my.choosevideo)（sourceType 包含 album）。 |
| scope.writePhotosAlbum | PermissionObject | 否 | 相册（保存）相关权限声明，相关 API：[my.saveImage](https://opendocs.alipay.com/mini/api/media/image/my.saveimage)、[my.saveImageToPhotosAlbum](https://opendocs.alipay.com/mini/api/media/image/my.saveImagetophotosalbum)、[my.saveVideoToPhotosAlbum](https://opendocs.alipay.com/mini/api/media/video/my.savevideotophotosalbum)。 |
| scope.camera | PermissionObject | 否 | 相机相关权限声明，相关 API：[my.chooseImage](https://opendocs.alipay.com/mini/api/media/image/my.chooseimage)、[my.chooseVideo](https://opendocs.alipay.com/mini/api/media/video/my.choosevideo)（sourceType 包含 camera）。 |
| scope.record | PermissionObject | 否 | 麦克风相关权限声明，相关 API：[my.getRecorderManager](https://opendocs.alipay.com/mini/api/getrecordermanager)。 |
| scope.userLocation | PermissionObject | 否 | 位置相关权限声明，相关 API：[my.getLocation](https://opendocs.alipay.com/mini/api/mkxuqd)。 |

## PermissionObject 结构

| **属性** | **类型** | **必填** | **描述**                             |
| -------- | -------- | -------- | ------------------------------------ |
| desc     | String   | 是       | 小程序获取权限时展示的接口用途说明。 |

### 使用示例

```JSON
{
  "permission": {
    "scope.album": {
      "desc": "读取照片用于提供美颜服务"
    },
    "scope.camera" : {
      "desc" : "访问你的摄像头，用于扫描二维码"
    },
    "scope.record" : {
      "desc" : "访问你的麦克风，用于识别歌曲"
    },
    "scope.userLocation": {
      "desc": "你的位置信息将用于匹配您的服务城市"
    },
    "scope.writePhotosAlbum" : {
      "desc" : "用于保存美颜后的照片"
    }
  }
}
```

![](https://gw.alipayobjects.com/mdn/rms_282813/afts/img/A*HTBCQrdaRvkAAAAAAAAAAAAAARQnAQ)

# behavior

用于改变小程序若干运行行为。字段类型为 Object，结构请见下方说明。

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| shareAppMessage | String | 否 | **可选值**：appendQuery。<br />使用小程序默认分享功能时（即不显式设置 [Page.onShareAppMessage](<https://opendocs.alipay.com/mini/framework/page-detail#onShareAppMessage(options%3A%20Object)>)），当设置此字段后，会使客户端生成的用于分享的 `scheme` 带上当前用户打开的页面所携带的 query 参数。<br />基础库 [2.7.10](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 及以上开始支持，同时需使用 [IDE 2.7.0](https://opendocs.alipay.com/mini/ide/download) 及以上版本进行构建。 |
| decodeQuery | String | 否 | **可选值**：disable。<br />小程序在解析全局参数、页面参数时默认会对键/值做 `encodeURIComponent`。当设置为 `disable` 后，则不再对键/值做`encodeURIComponent`，解析规则详情可查看 [小程序全局/页面参数设置以及解析细节](https://opendocs.alipay.com/mini/03durs)，基础库 [2.7.19](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 及以上开始支持，同时需使用 [IDE 3.0.0](https://opendocs.alipay.com/mini/ide/download) 及以上版本进行构建。 |

## 使用示例

```JSON
{
  "behavior": {
    "shareAppMessage": "appendQuery", // 通过此配置，可选择默认分享功能是否带上 query 参数。
    "decodeQuery": "disable" // 设置为disable后，基础库不再对全局/页面参数的键/值做 encodeURIComponent
  }
}
```

# 常见问题

## Q：A 页面（列表页）设置允许下拉刷新，B 页面（详情页）设置禁止下拉 `allowsBounceVertical: NO`, A 页面跳转 B 页面后再点左上角返回 A 页面，此时 A 页面无法下拉刷新。

A：A 页面设置下拉刷新的同时设置 `allowsBounceVertical: YES`,即可解决该问题。

**注意**：设置下拉刷新的时候一定要设置允许下拉。
