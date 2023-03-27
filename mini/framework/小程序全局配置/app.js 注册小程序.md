# App(object: Object)

`App()` 用于注册小程序，接受一个 `Object` 作为属性，用来配置小程序的生命周期等。`App()` 必须在 `app.js` 中调用，必须调用且只能调用一次。

# object 属性说明

| **属性** | **类型** | **描述** | **触发时机** | **基础库最低版本** |
| --- | --- | --- | --- | --- |
| onLaunch | Function | 生命周期回调：监听小程序初始化 | 当小程序初始化完成时触发，全局只触发一次。<br /> 参数也可以使用 [my.getLaunchOptionsSync](https://opendocs.alipay.com/mini/api/getLaunchOptionsSync) 获取。 | - |
| onShow | Function | 生命周期回调：监听小程序显示 | 当小程序启动，或从后台进入前台显示时触发。<br /> 也可以使用 [my.onAppShow](https://opendocs.alipay.com/mini/api/nn7do1)绑定监听。 | - |
| onHide | Function | 生命周期回调：监听小程序隐藏 | 当当前页面被隐藏时触发，例如跳转、按下设备 Home 键离开。<br />也可以使用 [my.onAppHide](https://opendocs.alipay.com/mini/api/tv6qvi) 绑定监听。 | - |
| onError | Function | 监听小程序错误 | 当小程序发生 js 错误时触发。<br /> 也可以使用 [my.onError](https://opendocs.alipay.com/mini/00nnsx) 绑定监听。 | - |
| onShareAppMessage | Function | 全局分享配置 | 调用分享时触发，如：点击页面菜单右上角的 **分享** 按钮时。 | - |
| onUnhandledRejection | Function | 监听 unhandledrejection 事件 | 当 Promise 被 reject 且没有 reject 处理器时，会触发 onUnhandledRejection 事件。<br />也可以使用 [my.onUnhandledRejection](https://opendocs.alipay.com/mini/00nd0f) 绑定监听。 | [1.24.1](https://opendocs.alipay.com/mini/framework/lib) |
| onPageNotFound | Function | 监听页面不存在 | 小程序要打开的页面不存在时触发。<br />也可以使用 [my.onPageNotFound](https://opendocs.alipay.com/mini/01zdng) 绑定监听。<br /> 不支持处理 [路由 API](https://opendocs.alipay.com/mini/api/fu8l65) 失败场景。 | [2.7.2](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) |

**前台/后台定义：**

- 一般情况下，小程序用户点击右上角关闭，或者按下设备 Home 键离开支付宝时，小程序并不会直接销毁，而是进入后台。
- 当用户再次进入支付宝或再次打开小程序时，小程序会从后台进入前台。
- 只有当小程序进入后台 5 分钟后，或占用系统资源过高，才会被真正销毁。
- 小程序是否销毁、是否进入后台，也与小程序自身业务逻辑、当前内存资源占用有关。

## onLaunch(object: Object) 及 onShow(object: Object)

object 属性说明：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| query | Object | 当前小程序的 query，从启动参数的 query 字段解析而来，解析规则可查看 [小程序全局 / 页面参数设置以及解析细节](https://opendocs.alipay.com/mini/03durs)。 |
| scene | String | 启动小程序的 [场景值](https://opendocs.alipay.com/mini/framework/scene)。 |
| path | String | 当前小程序的页面地址，从启动参数 page 字段解析而来，page 忽略时默认为首页。 |
| referrerInfo | Object | 来源信息。 |

比如，启动小程序的 scheme 如下:

```javascript
alipays://platformapi/startapp?appId=1999&query=number%3D1&page=x%2Fy%2Fz
```

- 小程序首次启动时，`onLaunch` 方法可获取 `query`、`path` 等属性值。

- 小程序处于后台时，如果从 scheme、扫二维码打开，需要在 `onShow` 方法中获取 `query`、`path` 等属性值。

```javascript
App({
  onLaunch(options) {
    // 第一次打开
    console.log(options.query);
    // {number:1}
    console.log(options.path);
    // x/y/z
  },
  onShow(options) {
    // 从后台被 scheme 重新打开
    console.log(options.query);
    // {number:1}
    console.log(options.path);
    // x/y/z
  },
});
```

`referrerInfo` 子属性说明：

| **属性**  | **类型** | **描述**                 | **最低版本** |
| --------- | -------- | ------------------------ | ------------ |
| appId     | String   | 来源小程序。             | -            |
| extraData | Object   | 来源小程序传过来的数据。 | -            |

**注意**：

- 不要在 `onShow()` 中进行 [my.redirectTo](https://opendocs.alipay.com/mini/api/fh18ky) 或 [my.navigateTo](https://opendocs.alipay.com/mini/api/zwi8gx) 等操作页面栈的行为。
- 不要在 `onLaunch()` 里调用 [getCurrentPages](https://opendocs.alipay.com/mini/framework/getcurrentpages) 方法，因为此时 `page` 还未生成。
- app.json 应用配置 `behavior` 支持配置项 `decodeQuery`，当设置为 `disable` 后，不会再对键值额外再做 `decodeComponent`，可查看 [小程序全局 / 页面参数设置以及解析细节](https://opendocs.alipay.com/mini/03durs)。

## onHide()

小程序从前台进入后台时触发 `onHide()` 。示例代码：

```javascript
App({
  onHide() {
    // 进入后台时
    console.log('app hide');
  },
});
```

## onError(error, stack)

小程序应用发生脚本错误时触发。事件也可以通过 [my.onError](https://opendocs.alipay.com/mini/00nnsx) 进行监听。其参数列表如下:

| **属性** | **类型** | **说明** |
| --- | --- | --- |
| error | String | 异常描述，一般为 `Error` 对象的 `message` 字段。 |
| stack | String | 异常堆栈，一般为 `Error` 对象的 `stack` 字段。<br /> 基础库 [2.6.6](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 及以上支持。 |

示例代码：

```javascript
App({
  onError(error, stack) {
    // 小程序执行出错时
    console.log(error);
    // 基础库2.6.6 开始支持stack参数
    console.error(stack);
  },
});
```

## onShareAppMessage(object: Object)

全局分享配置。当页面未设置 `page.onShareAppMessage` 时，调用分享会执行全局的分享设置，具体详情请参见 [页面事件处理函数](https://opendocs.alipay.com/mini/framework/page-detail#%E9%A1%B5%E9%9D%A2%E4%BA%8B%E4%BB%B6%E5%A4%84%E7%90%86%E5%87%BD%E6%95%B0)。

## onUnhandledRejection(object: Object)

当`Promise` 被 `reject` 且没有 `reject` 处理器时触发。也可使用 [my.onUnhandledRejection](https://opendocs.alipay.com/mini/00nd0f) 绑定监听。参数和注意事项与 [my.onUnhandledRejection](https://opendocs.alipay.com/mini/00nd0f) 一致。示例代码：

```javascript
App({
  onUnhandledRejection(res) {
    // 当小程序代码的Promise 被 reject 且没有 reject 处理器时触发。
    console.log(res.reason, res.promise);
    //res.reason 是reject原因，res.promise 是被reject的Promise对象
  },
});
```

## onPageNotFound(object: Object)

小程序要打开的页面不存在时触发。也可以使用 [my.onPageNotFound](https://opendocs.alipay.com/mini/01zdng) 绑定监听。参数和注意事项与 my.onPageNotFound 一致。示例代码：

```javascript
App({
  onPageNotFound(res) {
    my.redirectTo({
      url: '/pages/...',
    }); // 如果是 tabbar 页面，请使用 my.switchTab
  },
});
```

# globalData 全局数据

`App()` 中可以设置全局数据 `globalData`。示例代码：

```javascript
// app.js
App({
  globalData: 1,
});
```

# 更多

开发者可以添加任意的函数或数据变量到 Object 参数中，用 this 可以访问。

也可在 app.js 引入其他的公共方法，将方法挂载到 app.js 下。

示例代码：

```javascript
// app.js
import { getUserInfo } from '/utils/getOpenUserInfo';
App({
  onLaunch() {},
  onShow() {
    this.login(); // 通过this访问
  },
  // 自定义函数
  login() {
    console.log('自定义函数');
  },
  getUserInfo,
});
```

小程序页面调用：

```javascript
const app = getApp();
Page({
  onLoad() {
    app.getUserInfo();
    app.login(); // log输出 '自定义函数'
  },
});
```

# 常见问题

## Q：可以在 app.js 中关闭小程序吗？

A：不可以，关闭小程序的方法仅支持小程序页面点击右上角的关闭按钮。

# 相关文档

- [onShareAppMessage](https://opendocs.alipay.com/mini/framework/page-detail#%E9%A1%B5%E9%9D%A2%E4%BA%8B%E4%BB%B6%E5%A4%84%E7%90%86%E5%87%BD%E6%95%B0)
- [getApp 方法](https://opendocs.alipay.com/mini/framework/get-app)
