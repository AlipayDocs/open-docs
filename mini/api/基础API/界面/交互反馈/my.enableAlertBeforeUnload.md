
# 简介
开启小程序页面返回询问对话框。<br />调用后，用户点击页面左上角返回按钮时，会出现如下对话框：<br />![enable.png](https://cdn.nlark.com/yuque/0/2022/png/179989/1651127749522-3f26bd66-5891-4368-91dd-8cdbf2ccd36b.png#align=left&display=inline&height=107&margin=%5Bobject%20Object%5D&name=enable.png&originHeight=303&originWidth=849&size=26032&status=done&style=stroke&width=300)

## 使用限制

- 基础库 [2.7.17](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 及以上版本，客户端 10.2.60 及以上版本。若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。
- 不支持小程序插件内使用。
- 不支持在小程序首页调用。
- 小程序开发者工具（IDE）暂不支持调试此 API，请使用 [真机调试](https://opendocs.alipay.com/mini/ide/remote-debug) 功能在真机进行调试。

# 接口调用

## 示例代码

### .js 示例代码
```javascript
Page({
  onReady() {
    my.enableAlertBeforeUnload({
      message: '确认离开此页面?'
    })
  }
})

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
| **错误码** | **描述** | **解决方案** |
| --- | --- | --- |
| 7 | has not found page when enableAlertBeforeUnload has been invoked | 执行接口时小程序还未创建出任何一个页面实例，建议在 Page.onReady 回调内执行 my.enableAlertBeforeUnload。 |
| 8 | can not invoke enableAlertBeforeUnload at first page | 若某个页面比较复杂（即可能是第一个页面，也可能不是第一个页面），可以通过 [getCurrentPages](https://opendocs.alipay.com/mini/framework/getcurrentpages) 获取页面栈并判断当前页面实例是不是处于第一个。 |
| 9 | client not support enableAlertBeforeUnload | 一般不会出现，此时表明当前客户端不支持调用此接口，暂无解决方案。 |

<br />
