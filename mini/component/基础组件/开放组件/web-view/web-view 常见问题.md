## H5 页面相关

### 页面访问受限/报错/无法跳转的原因以及处理方法

- 不支持在小程序内加载 scheme 链接，scheme 链接无法被配置为业务域名。
- 不支持在小程序内加载支付宝官方 H5 链接，Alipay 的域名无法被配置为业务域名。
- 添加域名后需重新提交审核后发布才会生效。
- 域名仅支持 https 开头的链接，格式支持英文大小写字母、数字、及“-”，不支持 IP 地址及端口号。
- 配置域名后，请重新设置体验版或者推送真机预览。
- 需下载校验文件，并放置于配置域名的根目录下。
- 不支持 H5 页面为重定向页。
- 没有配置 H5 域名白名单，请参照 [配置 H5 域名](https://opendocs.alipay.com/mini/component/idfvg6) 完成配置，如遇白名单添加后仍然显示页面受限问题，请参见 [web-view 调试报错页面访问受限处理方法](https://opendocs.alipay.com/mini/component/access)。
- 支付宝 App 版本过低导致，升级至最新版本即可。

| **问题** | **方法** |
| --- | --- |
| H5 与小程序互相传递消息 | 请参考 [my.createWebViewContext](https://opendocs.alipay.com/mini/api/webview-context)。 |
| H5 跳转小程序首页 | 手动引入 `https://appx/web-view.min.js` (此链接仅支持在支付宝客户端内访问），再调用 [my.navigateTo](/mini/api/zwi8gx) 接口。 |
| web-view 内嵌的 H5 调用扫一扫 | 使用 web-view 与小程序的通信唤起 [my.scan](https://opendocs.alipay.com/mini/api/scan)。 |
| web-view 获取会员基础信息 | 在小程序页面通过 [button 组件](https://opendocs.alipay.com/mini/component/button) 授权属性唤起授权界面 [my.getOpenUserInfo](https://opendocs.alipay.com/mini/api/ch8chh) 将授权信息传送至 web-view 的 H5 页面。 |
| web-view 获取会员手机号 | 在小程序页面通过 [button 组件](https://opendocs.alipay.com/mini/component/button) 授权属性唤起授权界面 [my.getPhoneNumber](https://opendocs.alipay.com/mini/api/getphonenumber) 将授权信息传送至 web-view 的 H5 页面。 |
| web-view 获取授权码 | [my.getAuthCode](https://opendocs.alipay.com/mini/api/openapi-authorize)。 |
| 目前不支持截屏事件 | 支持 监听截屏 [my.onUserCaptureScreen](https://opendocs.alipay.com/mini/api/user-capture-screen)、取消监听截屏 [my.offUserCaptureScreen](https://opendocs.alipay.com/mini/api/umdxbg)。 |

### 如何处理 web-view 加载 H5 偶现白屏现象？

应该是 H5 网页样式的不适配，建议检查一下重新设置样式。

### 为何在 web-view 嵌入的 H5 中使用拼接 URL 方式进行用户授权报错访问受限？

不建议使用 web-view 嵌套 H5 进行 url 拼接授权，在 web-view 中使用 postmessage 发消息到小程序，小程序接收消息调用用户授权 API。

### web-view 内嵌的 H5 是否支持上传图片？

支持。可将获取到的图片路径通过 [my.postMessage()](https://opendocs.alipay.com/mini/component/web-view#%E5%8F%AF%E7%94%A8%20API) 将相关数据传递给小程序后进行图片上传。

### 小程序 web-view 如何打开小程序包内本地 html 文件 ？

web-view 只能打开 https 域名的 H5 链接。

### 小程序 web-view 开发阶段如何调试 H5 页面？

上线 H5 代码，IDE 模拟器中点击 web-view 进行调试。 <br />![](https://mdn.alipayobjects.com/afts/img/A*dA0CT569c2wAAAAAAAAAAABkAa8wAA/original?bz=openpt_doc&t=jd42Np9tqX-Zpb6c-BLZFAAAAABkMK8AAAAA#align=left&display=inline&height=194&margin=%5Bobject%20Object%5D&originHeight=194&originWidth=389&status=done&style=none&width=389)

### web-view 如何在本地开发调试传过来的数据？小程序支持外跳 H5 页面拉起支付吗？

可以使用本地搭建的环境测试。<br />不支持外跳，可以使用 web-view 嵌套 H5 页面，在 H5 页面中使用小程序支付的 API 来实现调起支付功能。

### 支付宝 H5 中设置的 cookie 与小程序 web-view 中的 cookie 是否共享？

H5 和 web-view 的 cookie 是不同的，小程序针对服务端回设的 cookie 不会禁用掉，会设置到小程序进程中，下次小程序进行请求，会自动将已有的 cookie 带入到服务端请求中。前端获取不到 cookie，也不会对 cookie 做任何操作。小程序不建议使用 cookie，推荐使用小程序缓存。

### web-view 嵌套的 H5 如何获取小程序缓存？web-view 如何清除缓存？web-view 如何读取小程序的 localstorage？

通过 web-view 内 H5 交互获取小程序缓存，具体请参见 [my.createWebViewContext](/mini/api/webview-context)。<br />可使用 [my.clearStorage](/mini/api/storage) 或者点击 IDE 右上角的 **清缓存** 清除缓存数据。如果是 web-view 总页面的缓存可以关闭小程序，重新打开支付宝。<br />web-view 的缓存和小程序缓存是隔离的，不能直接读取。都可以使用 API [my.clearStorage](/mini/api/storage) 清除缓存。

### H5 封装的小程序用 localstorage 设置的缓存，为何推出小程序取得的缓存是很早之前的数据？

web-view 页面存在缓存，建议动态链接访问最新地址。

### 为何商户小程序 web-view 打开 H5 页面请求抓不到包？

web-view 不支持抓包。可自行在 H5 页面中调试，保证 H5 显示没有问题后再放入 web-view 中打开。

### web-view 为首页的时候，H5 页面跳转没有返回按钮？

可使用 window.location 去跳转页面。

### 小程序中没有原生的小程序代码，是否可以通过 web-view 全部实现？

如果 H5 项目中没有调用 jsapi 而且也没有集团域名是可以实现的，但是不建议如此操作，建议开发原生小程序，小程序嵌套 H5 和独立 H5 体验都不如原生小程序。

### web-view 小程序和支付宝相互通信，是否支持互相一直发消息?

触发一次 H5 往小程序发，然后小程序往 H5 发一次。

### web-view 放在 tabbar 里面切换 tab 如何重新加载页面？

建议使用 H5 刷新页面的方式。

### H5 页面如何判断当前打开环境的方法？

判断是小程序的 web-view，还是支付宝内置浏览器可以使用 my.getEnv 接口，调用 my.getEnv 前需要在 H5 页面中引入 `https://appx/web-view.min.js` 依赖。

```javascript
//判断是否运行在小程序环境里
my.getEnv(function (res) {
  console.log(res.miniprogram); //true
});
```

### 通过 web-view 插入一个 H5 页面，为何使用 hidden 来实现显示/隐藏这个包裹 web-view 的元素不生效？

使用 a:if 可以实现显示/隐藏。a:if 与 hidden 对比区别请参见 [条件渲染](https://opendocs.alipay.com/support/01rb8w#%E6%9D%A1%E4%BB%B6%E6%B8%B2%E6%9F%93%EF%BC%8C%E5%AF%B9%E6%AF%94%20a%3Aif%20%E4%B8%8E%20hidden)。

## web-view 页面设计相关

- web-view 界面不支持显示 tips。<br />
- web-view 的标题取决于 H5 的标题，如需修改，请直接修改 H5 的标题内容。但是标题无法隐藏。<br />
- 一个 web-view 里面不能有太多嵌套，过多嵌套会影响性能，所以一般建议试图容器嵌套不超过 5 个。<br />
- 嵌套了 web-view 的页面加载过程中都会显示一个加载进度条，无法去掉。<br />
- web-view 中的 H5 的返回按钮不支持控制显示隐藏。 <br />

### 小程序分享成功后如何告知 web-view 组件分享成功的状态？

小程序中监听 [onShareAppMessage](https://opendocs.alipay.com/mini/framework/page-detail#%E9%A1%B5%E9%9D%A2%E4%BA%8B%E4%BB%B6%E5%A4%84%E7%90%86%E5%87%BD%E6%95%B0) 的 success 回调，然后传给 web-view。

### 为何在 web-view 页面添加按钮不显示？

web-view 的 H5 页面上不承载其他组件，即便添加也不会显示。

### web-view 页面嵌套小程序，为何获取手机号授权返回无效的授权方式？

web-view 无法使用小程序的 button 组件，所以会异常。

### 小程序 web-view 如何将数据存储到本地？ 

A：优先推荐 H5 本地存储 localStorage。如果需要跨域共享数据，可使用 [my.postMessage()](https://opendocs.alipay.com/mini/component/web-view#%E5%8F%AF%E7%94%A8%20API) 先将相关数据传递给小程序，再通过 [my.setStorage()](https://opendocs.alipay.com/mini/api/eocm6v) 存储。

## 开放能力

### 为何 web-view 使用图片上传跳回 web-view 首页？

在最近使用中删除该小程序，重新扫码调试。

### 小程序中是否可以引入第三方 URL 页面？

只要配置了业务域名就可以。

### 如何实现在 web-view 中跳转到其他小程序？

使用 web-view 与小程序通信交互，然后再小程序页面 js 中调用 [my.navigateToMiniProgram](/mini/api/yz6gnx) 跳转到其他小程序。

### web-view 中引入的 js 有本地文件吗？ js 只支持在线访问吗？ js 只能使用链接引入不能手动引入吗？

本地没有 js 文件，仅支持在支付宝客户端（小程序）内使用链接 H5 引入 ，不支持下载也不建议引用本地文件。

### web-view 支持刷新当前页面吗？

web-view 中没有该接口，可以重新请求数据从而更新页面。

### 小程序中可以调用支付宝开放平台的授权吗？

建议通过小程序与 web-view 交互的方式，由小程序获取手机号通过交互传给页面。

### 程序在控件显示上，能否在原生控件（地图控件）上叠加显示 web-view 控件？

不支持这样的操作。

### web-view 是否可以预览本地文件？

IDE 可预览本地文件，真机不支持。

### 为何 web-view 嵌套的 Html 内容已变更，但 IDE 中没有显示变更后的内容？

在嵌套的 Html 链接后面加上参数，使其不读取缓存，实现获取 Html 的最新内容。

### iOS 设备小程序 web-view 内播放视频退出小程序后视频仍然播放如何解决？

在页面隐藏时，通过 web-view 和 H5 双向通信，进行视频暂停。
