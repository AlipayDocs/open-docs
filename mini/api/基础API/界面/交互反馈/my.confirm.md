# 简介

**my.confirm** 是用于提示的确认框的 API，可以配置确认框的标题、内容、确认或取消按钮的文字等。

## 使用限制

此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验

![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/b24c2aeb8125978c77d93ab36157ac5e.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=none&width=127)

# 接口调用

## 示例

[小程序在线](https://opendocs.alipay.com/openbox/mini/opendocs/confirm?view=preview&defaultPage=pages/index/index&defaultOpenedFiles=pages/index/index&theme=light)

### .js 示例代码

```javascript
Page({
  comfirm() {
    my.confirm({
      title: '温馨提示',
      content: '您是否想查询快递单号：\n1234567890',
      confirmButtonText: '马上查询',
      cancelButtonText: '暂不需要',
      success: result => {
        my.alert({
          title: `${result.confirm}`,
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
| title | String | 否 | confirm 框的标题。 |
| content | String | 否 | confirm 框的内容。 |
| confirmButtonText | String | 否 | 确认按钮文字，默认为 **确定**。 |
| cancelButtonText | String | 否 | 取消按钮文字，默认为 **取消**。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

### Function success

success 回调函数会携带一个 Object 类型的对象，其属性如下：

| **属性** | **类型** | **描述**                                            |
| -------- | -------- | --------------------------------------------------- |
| confirm  | Boolean  | 点击确定按钮，返回 true；点击取消按钮，返回 false。 |
