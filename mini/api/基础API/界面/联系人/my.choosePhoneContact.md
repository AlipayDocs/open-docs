# 简介

**my.choosePhoneContact** 是选择系统通讯录中某个联系人电话的 API。

## 使用限制

此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验

![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/2af29e82e83aa4eeeac56c006dd2f79f.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=none&width=127)

# 接口调用

## 在线示例

[小程序在线](https://opendocs.alipay.com/openbox/mini/opendocs/contact?view=preview&defaultPage=pages/index/index&defaultOpenedFiles=pages/index/index&theme=light)

### .js 示例代码

```javascript

  choosePhoneContact() {
    my.choosePhoneContact({
      success: res => {
        my.alert({
          content: 'choosePhoneContact response: ' + JSON.stringify(res),
        });
      },
      fail: res => {
        my.alert({
          content: 'choosePhoneContact response: ' + JSON.stringify(res),
        });
      },
    });
  }
```

## 入参

Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

### success 回调函数

success 回调函数会携带一个 Object 类型的对象，其属性如下：

| **属性** | **类型** | **描述**             |
| -------- | -------- | -------------------- |
| name     | String   | 选中的联系人姓名。   |
| mobile   | String   | 选中的联系人手机号。 |

## 错误码

| **错误码** | **描述** | **解决方案** |
| --- | --- | --- |
| 2001 | 用户不允许授权。 | 同意授权支付宝使用通讯录。 |
| 11 | 用户取消操作（或设备未授权支付宝使用通讯录）。 | 非用户取消操作的情况下，建议设备授权使用通讯录。 |
