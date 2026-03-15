# 简介

可通过 web-view 组件在小程序中嵌入 H5 页面。小程序不直接支持外跳 H5，web-view 部分地满足跳转 H5 的需求。关于小程序跳转的内容可查看 [小程序内嵌&外跳能力导航](https://opendocs.alipay.com/mini/0090ty)。

web-view 可以打开的 H5 页面的域名限于开发者维护的 H5 域名白名单（开放平台控制台 > 小程序详情页 > 开发设置 > H5 域名配置），仅支持添加开发者可控制的域名。若 web-view 提示访问受限，可参考 [页面访问受限解决方案](https://opendocs.alipay.com/mini/component/access)。

开发过程中遇到问题可查看 [web-view 常见问题](https://opendocs.alipay.com/mini/component/mg7rvg)。

## 使用限制

- 支付宝客户端 10.1.35 或更高版本可用。
- **Native 渲染引擎**：基础库 [2.7.17](https://opendocs.alipay.com/mini/framework/compatibility)+，客户端 10.5.70+ 开始支持。可以通过 `my.canIUse('web-view')` 判断是否支持。
- 不支持个人小程序使用，仅支持企业小程序。
- 不支持在插件内使用。
- 每个页面只能有一个 web-view，会自动铺满整个页面并覆盖其它组件。
- 不支持多个页面 web-view 间通讯。不支持横屏以及全屏展示。
- 调试请以真机效果为准。

## 注意事项

- 包含中文等特殊字符的 URL，请先使用 encodeURL() 编码。
- 主文档 URL、iframe 里的主文档 URL，以及后续跳转的主文档 URL，其域名均需要加入 H5 域名白名单，否则无法访问。<br>
- H5 域名白名单维护方法请查看 [配置 H5 域名](https://opendocs.alipay.com/mini/component/idfvg6) 。不支持添加阿里（天猫、淘宝等）域名，且域名总数量不超过 50 个。<br>
- **H5 域名白名单变更后需要小程序发版，新的白名单仅对新版小程序生效。**

## 扫码体验

![](https://cdn.nlark.com/yuque/0/2022/png/179989/1646986480681-5129e778-2e51-411a-85f0-14a9c7d91c85.png)

## 效果示例

![](https://gw.alipayobjects.com/zos/skylark-tools/public/files/30af88e3aee4fad81364495deabe6307.png#align=left&display=inline&height=720&margin=%5Bobject%20Object%5D&originHeight=720&originWidth=1280&status=done&style=none&width=1280)

# 使用

## 示例代码

### .axml 示例代码

```html
<!-- API-DEMO page/component/webview/webview.axml -->
<view class="page">
  <web-view
    src="https://render.alipay.com/p/s/web-view/index"
    onMessage="onmessage"
  ></web-view>
</view>
```

### .js 示例代码

```javascript
// API-DEMO page/component/webview/webview.js
Page({
  data: {},
  onShareAppMessage(options) {
    my.alert({ content: JSON.stringify(options.webViewUrl) });
    return {
      title: '分享 web-View 组件',
      desc: 'View 组件很通用',
      path: 'page/component/component-pages/webview/baidu',
      'web-view': options.webViewUrl,
    };
  },
  onmessage(e) {
    my.alert({
      content: '拿到数据' + JSON.stringify(e), // alert 框的标题
    });
  },
});
```

## 属性说明

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| src | String | web-view 要渲染的 H5 网页 URL ，默认允许打开所有 `https://render.alipay.com/p/` 开头的 URL（支付宝客户端 10.2.63 版本开始支持），其他网页需要在 [开放平台控制台](https://openhome.alipay.com/develop/manage) > 对应小程序详情页 > **开发设置** > **H5域名配置** 进行 H5 域名白名单配置。<br />**说明**：src必须是标准的 H5 链接，任何包含例如 `alipays://xx...` 的链接都会导致重定向出错，从而无法展示页面，即使是 `https://render.alipay.com` 开头的 URL 也不能包含 `alipays://xx...` 此类内容。|
| onMessage | EventHandle | 网页向小程序 postMessage 消息。`e.detail = { data }` |
| onLoad | EventHandle | 网页加载成功时触发此事件。`e.detail = { src }`<br />**版本要求**：基础库 [2.7.3](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 及以上 |
| onError | EventHandle | 网页加载失败时触发此事件。`e.detail = { src }`<br />**版本要求**：基础库 [2.7.3](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 及以上 |

可以通过检测 `userAgent` 中包含 `MiniProgram` 字样来判断小程序 web-view 环境。

### 可用 API

web-view 载入的 H5 页面可以使用手动引入 https://appx/web-view.min.js（此链接仅支持在支付宝客户端内访问），提供了相关的 API 供您使用（**调试请以真机效果为准**）。

**说明：** 如需嵌入 H5 页面请使用表格中支持的 API，表格中如不支持请调用原生 js。

| **接口类别** | **接口名** | **描述** |
| --- | --- | --- |
| 导航栏 | [my.navigateTo](https://opendocs.alipay.com/mini/api/zwi8gx) | 保留当前页面，跳转到应用内的某个指定页面。 |
| 导航栏 | [my.navigateBack](https://opendocs.alipay.com/mini/api/kc5zbx) | 关闭当前页面，返回上一级或多级页面。 |
| 导航栏 | [my.switchTab](https://opendocs.alipay.com/mini/api/ui-tabbar) | 跳转到指定 tabBar 页面，并关闭其他所有非 tabBar 页面。 |
| 导航栏 | [my.reLaunch](https://opendocs.alipay.com/mini/api/hmn54z) | 关闭当前所有页面，跳转到应用内的某个指定页面。 |
| 导航栏 | [my.redirectTo](https://opendocs.alipay.com/mini/api/fh18ky) | 关闭当前页面，跳转到应用内的某个指定页面。 |
| 图片 | [my.chooseImage](https://opendocs.alipay.com/mini/api/media/image/my.chooseimage) | 拍照或从手机相册中选择图片（可将获取到的图片路径通过 `my.postMessage()` 将相关数据传递给小程序后进行图片上传）。 |
| 图片 | [my.previewImage](https://opendocs.alipay.com/mini/api/media/image/my.previewimage) | 预览图片。 |
| 位置 | [my.getLocation](https://opendocs.alipay.com/mini/api/mkxuqd) | 获取用户当前的地理位置信息。 |
| 位置 | [my.openLocation](https://opendocs.alipay.com/mini/api/as9kin) | 使用支付宝内置地图查看位置。 |
| 交互反馈 | [my.alert](https://opendocs.alipay.com/mini/api/ui-feedback) | 警告框。 |
| 交互反馈 | [my.showLoading](https://opendocs.alipay.com/mini/api/bm69kb) | 显示加载提示。 |
| 交互反馈 | [my.hideLoading](https://opendocs.alipay.com/mini/api/nzf540) | 隐藏加载提示。 |
| 网络状态 | [my.getNetworkType](https://opendocs.alipay.com/mini/api/network-status) | 获取当前网络状态。 |
| 分享 | my.startShare | 分享当前页面,当执行 my.startShare() 时会唤起当前小程序页面的分享功能。 |
| 唤起支付 | [my.tradePay](https://opendocs.alipay.com/mini/api/openapi-pay) | 唤起支付（仅支持使用该 API 唤起支付，不支持使用 H5 进行支付） |
| 向小程序发送消息 | my.postMessage | 向小程序发送消息，自定义一组或多组 key 、 value 数据，格式为 JSON ，如：`my.postMessage({name:"测试web-view"})`。 |
| 监听小程序发过来的消息 | my.onMessage | 监听小程序发过来的消息， [webview 组件控制](https://opendocs.alipay.com/mini/api/webview-context)。 |
| 获取当前环境 | my.getEnv | 获取当前环境。 |

### 示例代码

web-view H5 页面代码：

```javascript
<script type="text/javascript" src="https://appx/web-view.min.js"></script>
<!-- 如该 H5 页面需要同时在非支付宝客户端内使用，为避免该请求404，可参考以下写法 -->
<!-- 请尽量在 html 头部执行以下脚本 -->
<script>
  if (navigator.userAgent.indexOf('AliApp') > -1) {
    document.writeln('<script src="https://appx/web-view.min.js"' + '>' + '<' + '/' + 'script>');
  }
</script>
<script>
  my.navigateTo({url: '../get-user-info/get-user-info'});
  // 网页向小程序 postMessage 消息
  my.postMessage({name:"测试web-view"});
  // 接收来自小程序的消息。
  my.onMessage = function(e) {
    console.log(e); // {'sendToWebView': '1'}
  }
  // 判断是否运行在小程序环境里
  my.getEnv(function(res) {
    console.log(res.miniprogram) // true
  });
  my.startShare();
</script>
```

my.postMessage 信息发送后，小程序页面接收信息时，会执行 onMessage 配置的方法：

```html
<!-- .axml -->
<view>
  <web-view id="web-view-1" src="..." onMessage="test"></web-view>
</view>
```

```javascript
// 小程序页面对应的 page.js 声明 test 方法，
// 由于 page.axml 里的 web-view 组件设置了 onMessage="test",
// 当页面里执行完 my.postMessage 后，test 方法会被执行
Page({
  onLoad(e) {
    this.webViewContext = my.createWebViewContext('web-view-1');
  },
  test(e) {
    my.alert({
      content: JSON.stringify(e.detail),
    });
    this.webViewContext.postMessage({ sendToWebView: '1' });
  },
});
```

用户分享时可获取当前 web-view 的 URL ，即在 onShareAppMessage 回调中返回 webViewUrl 参数。

```javascript
Page({
  onShareAppMessage(options) {
    console.log(options.webViewUrl);
  },
});
```
