# 简介
**my.navigateToMiniProgram** 是用于跳转到其它小程序的 API。

目标小程序可通过 [联调设置](https://opendocs.alipay.com/mini/ide/integration-testing) 来唤起指定的开发版本。

相关问题可查看 [小程序相互跳转 FAQ](https://opendocs.alipay.com/mini/api/xqvxl4)。

## 使用限制
此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码
```javascript
// .js
my.navigateToMiniProgram({
      appId: 'xxxx',
      path: 'pages/index/index',
      extraData:{
        "data1":"test"
      },
      success: (res) => {
        console.log(JSON.stringify(res))
      },
      fail: (res) => {
        console.log(JSON.stringify(res))
      }
    });
```

## 入参
Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| appId | String | 是 | 要跳转的目标小程序 appId。 |
| path | String | 否 | 打开的页面路径，如果为空则打开首页。<br />path 中 ? 后内容会成为页面参数，在小程序的 `Page.onLoad(query)` 回调函数中可以获取到页面参数，解析规则可查看 [小程序全局 / 页面参数设置以及解析细节](https://opendocs.alipay.com/mini/03durs)。 |
| query | Object | 否 | 用于设置目标小程序的全局参数，目标小程序可通过 `App.onLaunch()`、`App.onShow()` 、`my.getLaunchOptionsSync()` 获取到全局参数。<br />基础库 [2.7.19](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 开始支持。 |
| extraData | Object | 否 | 需要传递给目标小程序的数据库，为键值对的格式，数值的类型为字符串。<br />目标小程序可在 `App.onLaunch()`、`App.onShow()` 中获取到这份数据。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

## 错误码
| **错误码** | **描述** | **解决方案** |
| --- | --- | --- |
| 30 | 目标应用不允许被跳转。 | 需检查目标应用跳转设置，登录 [开放平台控制台](https://open.alipay.com/dev/workspace) > 点击要设置的小程序，进入小程序详情页 > **设置** > **基础设置** > **小程序互相跳转** 中设置 **允许所有小程序跳转** 或 **指定小程序跳转**。 |
| 31 | 跳转失败。 | 可能是目标应用信息查询失败导致，建议检查跳转的目标应用是否已经上架。<br />**注意**：APPID 长度为 8 位的小程序暂不支持跳转。 |

# 常见问题 FAQ

## Q：my.navigateToMiniProgram 的 extraData 的参数在哪里获取？ extraData 是否可以添加多个参数？自定义参数中间使用的什么符号进行拼接？如何获取自定义的参数
A：目标小程序可在 App.onLaunch( )、App.onShow( ) 中获取到这份数据。extraData可以是一个包含多个参数的对象。

```js
// 跳转小程序示例代码
my.navigateToMiniProgram({
  appId: 'targetAppId',
  extraData: {
    key1: 'some data',
    key2: {
      foo: 'bar'
    }
  }
})

// 获取extraData示例代码
App({
  onLaunch(options) {
    const { referrerInfo = {}, appId } = options
    const { key1, key2 } = referrerInfo.extraData || {}
  }
});

```

## Q：小程序如何唤起小程序营销活动？
A：可查看 [小程序营销](https://opendocs.alipay.com/mini/operation/app-with-benefit)。
