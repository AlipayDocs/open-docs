# 简介

my.enableAlertBeforeUnload 开启小程序页面返回询问对话框。

调用后，用户尝试关闭当前小程序页面时会出现如下对话框：

<img src="https://mdn.alipayobjects.com/huamei_esgcm9/afts/img/A*DWmQQbYZLtAAAAAAAAAAAAAADsaJAQ/original" width="300px"/>

## 使用限制

- 基础库 [2.7.17](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 及以上版本，客户端 10.2.60 及以上版本。若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。
- 不支持小程序插件内使用。
- 不支持在小程序首页调用。
- 用户通过 Home 键或右上角胶囊按钮的“×”退出小程序时不会触发询问对话框。
- 小程序开发者工具（IDE）暂不支持调试此 API，请使用 [真机调试](https://opendocs.alipay.com/mini/ide/remote-debug) 功能在真机进行调试。

# 接口调用

## 示例代码

### .js 示例代码

```javascript
Page({
  onReady() {
    my.enableAlertBeforeUnload({
      message: '确认离开此页面?',
    });
  },
});
```

## 参数

Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| message | String | 是 | 询问对话框内容。<br />**默认值**："离开此页面?"。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

## 错误码

fail 回调将收到一个 Object 类型的参数，其 error 属性为错误码，errorMessage 为错误消息

| **错误码** | **错误消息** | **解决方案** |
| --- | --- | --- |
| 7 | has not found page when enableAlertBeforeUnload has been invoked | 请在 Page.onReady 以后调用。 |
| 8 | can not invoke enableAlertBeforeUnload at first page | 不支持在首页调用此接口，请在非首页代码中调用。 |
| 9 | client not support enableAlertBeforeUnload | 当前客户端版本不支持此接口，可忽略此报错或酌情提示升级。 |

