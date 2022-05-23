
# 简介
**my.createWebViewContext** 是通过创建 `webviewContext` 提供从小程序向 `web-view` 发送消息的能力的 API。创建并返回  `web-view` 上下文 `webViewContext` 对象。

## 使用限制

- 基础库 [1.8.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端  10.1.10 或更高版本，若版本较低，建议采取 [兼容处理](/mini/framework/compatibility)。 
- 此 API 暂仅支持企业支付宝小程序使用。

# 接口调用

## 示例代码
**说明**：该示例代码的双向通信能力的流程是 H5 先发消息给小程序，小程序接收到消息后再发消息给 H5。

### .axml 示例代码
```html
<!-- .axml -->
<view>
  <web-view id="web-view-1" src="..." onMessage="onMessage"></web-view>
</view>
```

### .js 示例代码
```javascript
// .js
Page({
  onLoad() {
    this.webViewContext = my.createWebViewContext('web-view-1');
  },
  // 接收来自H5的消息
  onMessage(e) {
    console.log(e); //{'sendToMiniProgram': '0'}
    // 向H5发送消息
  this.webViewContext.postMessage({'sendToWebView': '1'});
  }
})
```
```javascript
// .js
// H5的js代码中需要先定义my.onMessage 用于接收来自小程序的消息。
my.onMessage = function(e) {
  console.log(e); //{'sendToWebView': '1'}
}
// H5向小程序发送消息
my.postMessage({'sendToMiniProgram': '0'});
```

**注意**，代码示例中的 `my.onMessage = ` 是一个赋值操作，当 H5 收到来自小程序的消息时，会执行 my.onMessage 接口，调用您所定义的函数。

## 入参
Object 类型，属性如下：

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| webviewId | String | 是 | 要创建的 `web-view` 所对应的 ID 属性。 |


## 返回值
为一个 webViewContext 对象。

`webViewContext` 通过 webviewId 跟一个 [web-view](https://opendocs.alipay.com/mini/component/web-view) 组件绑定，通过它可以实现一些功能。`webViewContext`对象的方法列表：

| **方法名** | **类型** | **描述** |
| --- | --- | --- |
| postMessage | Object | 小程序向 `web-view` 组件发送消息，配合 web-view.js 中提供的 my.postMessage 可以实现小程序和 web-view 网页的双向通信。<br />基础库 [1.8.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本开始支持。 |

