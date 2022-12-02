# 简介

**my.showToast** 是显示一个弱提示的 API。

## 使用限制

此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验

![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/e9f3b3c8c7c3cd7d169955c9facf59fa.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=none&width=127)

# 接口调用

## 在线示例

[小程序在线](https://opendocs.alipay.com/openbox/mini/opendocs/toast?view=preview&defaultPage=pages/index/index&defaultOpenedFiles=pages/index/index&theme=light)

### .js 示例代码

```javascript
// toast.js
Page({
  showToastSuccess() {
    my.showToast({
      type: 'success',
      content: '操作成功',
      duration: 3000,
      success: () => {
        my.alert({
          title: 'toast 消失了',
        });
      },
    });
  },
});
```

## 入参

Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| content | String | 否 | 文字内容。 |
| type | String | 否 | 根据 type 类型，展示相应图标，默认值为 none。可选值如下：<ul><li>success</li><li>fail</li><li>exception</li><li>none</li></ul> 其中 exception 类型必须传文字信息。 |
| duration | Number | 否 | 显示时长，单位为 ms，默认值为 3000。 |
| mask | Boolean | 否 | 是否显示透明蒙层，防止触摸穿透，默认值为 false。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

## 错误码
fail 回调会收到一个 Object 类型的参数，其 error 属性为错误码，errorMessage 为错误消息。
| **错误码** | **错误信息** | **解决方案** |
| --- | --- | --- |
| 2 | INVALID_PARAM | 请检查入参，传入正确的参数。 |
