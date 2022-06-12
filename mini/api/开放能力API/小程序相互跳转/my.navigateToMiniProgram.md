# 简介

**my.navigateToMiniProgram** 是用于跳转到其它小程序的 API。

如需跳转到目标小程序的指定开发版本，请参考 [联调设置](https://opendocs.alipay.com/mini/ide/integration-testing)

有关小程序跳转的更多知识，可查看 [小程序相互跳转 FAQ](https://opendocs.alipay.com/mini/api/xqvxl4)。 

## 使用限制

此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

```javascript
// 跳转小程序示例代码
my.navigateToMiniProgram({
  appId: 'xxxxxxxxxxxxxxx',
  path: 'pages/index/index?p=1&q=2', 
  query: {
    a: 'foo',
    b: 'bar',
  },
  extraData: {
    x: {
      y: 'z'
    },
  },
  success: () => {
    console.log('navigateToMiniProgram success');
  },
  fail: (res) => {
    my.alert({
      title: 'navigateToMiniProgram fail',
      content: JSON.stringify(res),
    });
  }
});

// 目标小程序获取页面参数
Page({
  onLoad(query) {
    console.log('query:', query); // query: { p: 1, q: 2 }
  },
});

// 目标小程序获取应用参数
App({
  onLaunch(options) {
    const { query, referrerInfo: { extraData } = {} } = options;
    console.log('query:', query); // query: { a: 'foo', b: 'bar' }
    console.log('extraData:', extraData); // extraData: { x: { y: 'z' } }
  },
  onSomeButtonTap() {
    const { query, referrerInfo: { extraData } = {} } = my.getLaunchOptionsSync();
    // ...
  },
});

```

## 入参
Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| appId | String | 是 | 要跳转的目标小程序 appId |
| path | String | 否 | 要打开的目标小程序页面路径。省略此参数则打开目标小程序首页。<br />path 中`?`后的内容会被解析为页面的 query 参数，目标小程序可在 `Page.onLoad(query)` 中获取。参数解析规则可参考 [小程序全局 / 页面参数设置以及解析细节](https://opendocs.alipay.com/mini/03durs)。 |
| query | Object | 否 | 传给目标小程序启动参数的 query 字段，目标小程序可在 `App.onLaunch(options)` 或 `App.onShow(options)` 中通过 options.query 获取，也可通过 my.getLaunchOptionsSync().query 获取。<br />基础库从 2.7.19 开始支持此参数，使用 1.x 版本的小程序需要 [升级基础库](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2)。 |
| extraData | Object | 否 | 传给目标小程序的额外数据。<br />目标小程序可在 `App.onLaunch(options)` 或 `App.onShow(options)` 中通过 options.referrerInfo?.extraData 获取。 |
| success | Function | 否 | 调用成功的回调函数。|
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

## 错误码
| **错误码** | **描述** | **解决方案** |
| --- | --- | --- |
| 30 | 目标应用不允许被跳转。 | 检查目标小程序的设置。操作路径：[开放平台控制台](https://open.alipay.com/dev/workspace) > 点击要设置的小程序，进入小程序详情页 > **设置** > **基础设置** > **小程序互相跳转** 中设置 **允许所有小程序跳转** 或 **指定小程序跳转**。 |
| 31 | 跳转失败。 | 检查 appId 参数。appId 为 16 位数字，由开放平台在小程序创建时分配。<br>注意：如果目标小程序未上架，调用本接口仍会触发 success 回调而非失败报错，未通过 [联调设置](https://opendocs.alipay.com/mini/ide/integration-testing) 指定跳转开发版的用户将看到 “暂未找到此功能” 提示页 |

# 常见问题 FAQ

## Q：小程序如何唤起小程序营销活动？
A：可查看 [小程序营销](https://opendocs.alipay.com/mini/operation/app-with-benefit)。
