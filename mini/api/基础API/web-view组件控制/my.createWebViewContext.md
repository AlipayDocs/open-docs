# 简介

**my.createWebViewContext** 是通过创建 `WebViewContext` 提供从小程序向 [web-view 组件](https://opendocs.alipay.com/mini/component/web-view) 发送消息的能力的 API。创建并返回指定 `web-view` 上下文的 `WebViewContext` 对象。

本文档仅介绍了 `my.createWebViewContext` 的使用方法，更多 web-view 相关问题，请查看 [web-view 组件](https://opendocs.alipay.com/mini/component/web-view) 的文档。

## 使用限制

- 基础库 [1.8.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.10 或更高版本，若版本较低，建议采取 [兼容处理](/mini/framework/compatibility)。
- 此 API 暂仅支持企业支付宝小程序使用。

# 接口调用

## 示例代码

**说明**：该示例代码演示了如何与 web-view 进行双向通信。

在 H5 调用 `my.postMessage` 发消息给小程序，小程序在 onMessage 方法中可以接收到消息。

在小程序中调用 `this.webViewContext.postMessage` 可以向对应的 web-view 组件发送消息，在 web-view 中的 H5 上可以通过定义一个 `my.onMessage` 函数接收到消息。

### .axml 示例代码

```html
<!-- page.axml -->
<view>
  <web-view id="web-view-1" src="https://..." onMessage="onMessage"></web-view>
</view>
```

### .js 示例代码

```javascript
// page.js
// 小程序页面对应的 page.js 声明一个 onMessage 方法，
// 在 page.axml 中的 web-view 组件设置属性 onMessage="onMessage",
// 当 web-view 中的 js 执行完 my.postMessage 后；小程序页面接收到消息时，会执行 onMessage 方法
Page({
  onLoad() {
    this.webViewContext = my.createWebViewContext('web-view-1');
  },
  // 接收来自H5的消息
  onMessage(e) {
    // e.detail 是 H5 发来的消息内容
    console.log(e.detail);
    // 向H5发送消息
    this.webViewContext.postMessage({ sendToWebView: '1' });
  },
});
```

web-view 所加载的 H5 页面中的 js 代码：

```javascript
// H5 的 js 代码
// 需要定义 my.onMessage 函数用于接收来自小程序的消息
my.onMessage = function (message) {
  // 这里收到的 message 就是小程序原样发过来的
  console.log(message);
};
// H5 向小程序发送消息
my.postMessage({ sendToMiniProgram: '0' });
```

**请注意**，代码示例中的 `my.onMessage =` 是一个赋值操作，当 H5 收到来自小程序的消息时，会尝试执行 my.onMessage 函数，也就会调用您所定义的函数。

## 入参

Object 类型，属性如下：

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| webviewId | String | 是 | 要创建的 `web-view` 所对应的 id 属性。在上面的代码示例中，webviewId 为 `web-view-1`。 |

## 返回值

为一个 `WebViewContext` 对象。

`WebViewContext` 通过 webviewId 与一个 [web-view 组件](https://opendocs.alipay.com/mini/component/web-view) 绑定，随后可以与对应的 `web-view` 组件进行通信。

`WebViewContext` 对象的方法列表：

| **方法名** | **类型** | **描述** |
| --- | --- | --- |
| postMessage | Object | 小程序向 `web-view` 组件发送消息，配合 web-view.js 中提供的 my.postMessage 可以实现小程序和 web-view 网页的双向通信。<br />基础库 [1.8.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本开始支持。 |
