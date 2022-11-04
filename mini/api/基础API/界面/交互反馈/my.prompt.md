# 简介

**my.prompt** 是弹出一个对话框，让用户在对话框内输入文本的 API。

## 使用限制

- 基础库 [1.7.2](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.10 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 在线示例

[小程序在线](https://opendocs.alipay.com/openbox/mini/opendocs/prompt?view=preview&defaultPage=pages/index/index&defaultOpenedFiles=pages/index/index&theme=light)

### .js 示例代码

```javascript
// .js
my.prompt({
  title: '标题单行',
  message: '说明当前状态、提示用户解决方案，最好不要超过两行。',
  placeholder: '给朋友留言',
  okButtonText: '确定',
  cancelButtonText: '取消',
  confirmColor: "#49a9ee",
  cancelColor: "#000000",
  success: result => {
    my.alert({
      title: JSON.stringify(result),
    });
  },
});
```

## 入参

Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| title | String | 否 | 提示框的标题。 |
| message | String | 否 | 提示框的显示内容，默认为 **请输入内容**。 |
| align | String | 否 | 提示框显示内容的对齐方式。<br />可选值为：left 、center 、right。 |
| placeholder | String | 否 | 输入框内的提示文案。 |
| okButtonText | String | 否 | 确认按钮文字，默认值为 **确定**。 |
| cancelButtonText | String | 否 | 取消按钮文字，默认值为 **取消**。 |
| confirmColor | String | 否 | 确认按钮的文字颜色，必须是 16 进制格式的颜色字符串，例 "#49a9ee"。 |
| cancelColor | String | 否 | 取消按钮的文字颜色，必须是 16 进制格式的颜色字符串，例 "#000000"。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

### Function success

success 回调函数会携带一个 Object 类型的对象，其属性如下：

| **属性**   | **类型** | **描述**                                    |
| ---------- | -------- | ------------------------------------------- |
| ok         | Boolean  | 点击确认按钮返回 true，点击取消按钮返回 false。 |
| inputValue | String   | 当点击确认按钮时，返回用户输入的内容。 |

# 常见问题

## Q：如何隐藏 my.prompt 的输入框？

A：不支持隐藏，若仅需弹出对话框，可使用 [my.alert](https://opendocs.alipay.com/mini/api/ui-feedback)。
