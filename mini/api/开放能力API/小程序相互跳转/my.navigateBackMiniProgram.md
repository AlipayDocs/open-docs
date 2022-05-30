# 简介
**my.navigateBackMiniProgram** 是用于跳转回上一个小程序的 API。只有当前小程序是由其他小程序跳转而来，调用此 API 才有效果。

更多小程序互相跳转问题，可查看 [小程序相互跳转 FAQ](https://opendocs.alipay.com/mini/api/xqvxl4)。

## 使用限制
此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

```javascript
// 接口调用示例
my.navigateBackMiniProgram({
  extraData: {
    'foo': 'bar'
  },
  success: (res) => {
    console.log(JSON.stringify(res))
  }
});

// 目标小程序接收 extraData 示例
App({
  onShow(options) {
    const { referrerInfo = {}, appId } = options;
    console.log('extraData: ', referrerInfo.extraData);
  }
});
```

## 入参
Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| extraData | Object | 否 | 需要传递给上目标小程序的数据。<br>目标小程序可在 App.onShow(options) 中从通过 options.referrerInfo.extraData 获取。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

# 已知问题

1. `bug` 如果当前小程序不是由其他小程序调起，调用此 API 既不会发生跳调转，也不会触发 fail/complete 回调
2. `bug` Android 上真机预览/真机调试对此 API 支持有缺陷，不能正常回到前一个小程序（会停在白屏）
