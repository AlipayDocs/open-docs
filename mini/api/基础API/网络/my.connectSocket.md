# 简介

**my.connectSocket** 用于创建 [WebSocket](https://developer.mozilla.org/zh-CN/docs/Web/API/WebSocket) 的连接。

## 使用限制

此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验

![](https://gw.alipayobjects.com/zos/skylark-tools/public/files/adccc0ecd4072e1b0fccc2cacf01ec8d.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=stroke&width=127)

## 效果示例

![](https://gw.alipayobjects.com/zos/skylark-tools/public/files/fc3f122b0dbbcef4cb9d4b17f5bb0232.png#align=left&display=inline&height=420&margin=%5Bobject%20Object%5D&originHeight=720&originWidth=1280&status=done&style=stroke&width=746)

# 接口调用

## 示例代码
**注意**：案例仅供参考，建议使用自己的地址进行测试。

### 单实例
```javascript
// .js
my.connectSocket({
  url: this.data.websocketServer, // 开发者服务器接口地址，必须是 wss 协议，且域名必须是后台配置的合法域名
  data: {},
  header:{
    'content-type': 'application/json'
  },
  success: (res) => {
     console.log('WebSocket 连接成功');
  },
  fail: () => {
     my.showToast({
        content: 'fail', // 文字内容
     });
  }
});
```

### 多实例
入参传递 multiple = true 时，可返回一个 SocketTask 实例，可以据此同时进行多个 WebSocket 连接。下面的例子展示了两个实例的使用场景：<br />**index.axml **示例代码：
```html
<button size="default" type="primary" onTap="connectSocket1">connectSocket1</button>
<button size="default" type="primary" onTap="connectSocket2">connectSocket2</button>

<button size="default" type="primary" onTap="onSocketMessage">监听两个 Weboscket 的消息</button>

<button size="default" type="primary" onTap="sendSocketMessage1">sendSocketMessage1</button>
<button size="default" type="primary" onTap="sendSocketMessage2">sendSocketMessage2</button>
```
**index.js** 示例代码：
```javascript
let socketTask1 = null;
let socketTask2 = null;
Page({
  //创WebSocket 连接
  connectSocket1() {
    socketTask1 = my.connectSocket({
      url: '您的 WebSocket 地址',
      multiple: true,
      success: (res) => {
        socketTask1.onOpen((openRes) => {
          console.log('socketTask1: 监听到连接开启')
        })
      }
    });
  },
  connectSocket2() {
    socketTask2 = my.connectSocket({
      url: '您的 WebSocket 地址',
      multiple: true,
      success: (res) => {
        socketTask2.onOpen((openRes) => {
          console.log('socketTask2: 监听到连接开启')
        })
      }
    });
  },
  //发送数据，必须先创建连接，才可以正常发送数据成功
  sendSocketMessage1() {
    socketTask1.send({
      data: 'socketTask1 发送的消息',
    });
  },
  //发送数据，必须先创建连接，才可以正常发送数据成功
  sendSocketMessage2() {
    socketTask2.send({
      data: "socketTask2 发送的消息"
    });
  },
  //监听WebSocket接受到服务器的消息事件
  onSocketMessage() {
    socketTask1.onMessage((res) => {
      console.log(`socketTask1: 监听到收到服务器内容：` + JSON.stringify(res.data));
    });
    socketTask2.onMessage((res) => {
      console.log(`socketTask2: 监听到收到服务器内容：` + JSON.stringify(res.data));
    });
    console.log('开启监听')
  },

  //关闭WebSocket连接
  closeSocket() {
    socketTask1.close({
      code: 1000,
      reason: "socketTask1 正常关闭",
      success: (res) => {
        console.log('关闭连接')
      },
    });
    socketTask2.close({
      code: 1000,
      reason: "socketTAsk2 正常关闭",
      success: (res) => {
        console.log('关闭连接')
      },
    });
  },
  //监听WebSocket关闭
  onSocketClose() {
    socketTask1.onClose((res) => {
      console.log(`监听到 socketTask1 已关闭！` + JSON.stringify({ res }));
    });
  },
  //监听WebSocket关闭
  onSocketClose() {
    socketTask2.onClose((res) => {
      console.log(`监听到 socketTask2 已关闭！` + JSON.stringify({ res }));
    });
  },
})
```
代码中 url 参数需要替换成实际开发使用的 WebSocket 地址。依次点击下图中的五个按钮，即可依次完成两个 SocketTask 任务的连接、消息监听、消息发送流程。

![3.png](https://cdn.nlark.com/yuque/0/2022/png/179989/1663898594798-846ef34c-0923-416d-9847-020db4926963.png#align=left&display=inline&height=464&margin=%5Bobject%20Object%5D&name=3.png&originHeight=788&originWidth=1530&size=203255&status=done&style=none&width=900)

若使用的 WebSocket 地址可将消息进行广播转发的话，控制台输出如下：

![4.png](https://cdn.nlark.com/yuque/0/2022/png/179989/1663898625923-8cf248d4-acd6-4e76-a68c-5b7d42b57bf1.png#align=left&display=inline&height=250&margin=%5Bobject%20Object%5D&name=4.png&originHeight=344&originWidth=1240&size=98938&status=done&style=none&width=900)

## 入参
Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| url | String | 是 | 目标服务器接口地址。<br />**注意：** 部分新发布的小程序只支持 wss 协议。 |
| data | Object | 否 | 请求的参数。 |
| header | Object | 否 | 设置请求的头部。 |
| multiple | Boolean | 否 | 是否多实例。传入 true 时，将返回一个包含 SocketTask 实例。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

## SocketTask
SocketTask 指 WebSocket 任务，可通过 my.connectSocket 接口传入参数 multiple = true 创建返回，以支持多实例的 WebSocket 连接。此时，该接口的返回值是一个 SocketTask 实例，所有和当前连接有关的方法、事件将通过该实例进行管理，不再直接通过 my 变量进行管理。

### SocketTask.send(Object object)
通过 WebSocket 发送数据。接口参数同 [my.sendSocketMessage](https://opendocs.alipay.com/mini/api/mr91d1)。

### SocketTask.close(Object object)
关闭 WebSocket 连接。接口参数同 [my.closeSocket](https://opendocs.alipay.com/mini/api/network)。

### SocketTask.onOpen(function callback)
监听 WebSocket 连接打开事件。接口参数同 [my.onSocketOpen](https://opendocs.alipay.com/mini/api/itm5og)。

### SocketTask.onClose(function callback)
监听 WebSocket 连接关闭事件。接口参数同 [my.onSocketClose](https://opendocs.alipay.com/mini/api/foqk6g)。

### SocketTask.onError(function callback)
监听 WebSocket 错误事件。接口参数同 [my.onSocketError](https://opendocs.alipay.com/mini/api/giu3c2)。

### SocketTask.onMessage(function callback)
监听 WebSocket 接受到服务器的消息事件。接口参数同 [my.onSocketMessage](https://opendocs.alipay.com/mini/api/gecnap)。

### SocketTask.offOpen(function callback)
取消监听 WebSocket 连接打开事件。接口参数同 [my.offSocketOpen](https://opendocs.alipay.com/mini/api/dva3t8)。

### SocketTask.offClose(function callback)
取消监听 WebSocket 连接关闭事件。接口参数同 [my.offSocketClose](https://opendocs.alipay.com/mini/api/qc4q3t)。

### SocketTask.offError(function callback)
取消监听 WebSocket 错误事件。接口参数同 [my.offSocketError](https://opendocs.alipay.com/mini/api/kk7vv7)。

### SocketTask.offMessage(function callback)
取消监听 WebSocket 接受到服务器的消息事件。接口参数同 [my.offSocketMessage](https://opendocs.alipay.com/mini/api/roziyq)。

## 错误码
| **错误码** | **描述** | **解决方案** |
| --- | --- | --- |
| 1 | 未知错误。 | - |
| 2 | 网络连接已经存在。 | 请在调用 connectSocket 接口时，传入参数 multiple = true 以创建多个 SocketTask 实例。不传递该参数的连接只能创建一次。  |
| 3 | URL 参数为空。 | 替换 URL 链接。 |
| 4 | 无法识别的 URL 格式。 | 替换 URL 链接。 |
| 5 | URL 必须以 ws 或者 wss 开头。 | 替换 URL 链接。 |
| 6 | 连接服务器超时。 | 稍后重试。 |
| 7 | 服务器返回的 https 证书无效。 | 小程序必须使用 HTTPS/WSS 发起网络请求。请求时系统会对服务器域名使用的 HTTPS 证书进行校验，如果校验失败，则请求不能成功发起。由于系统限制，不同平台对于证书要求的严格程度不同。为了保证小程序的兼容性，建议开发者按照最高标准进行证书配置，并使用相关工具检查现有证书，确保其符合要求。 |
| 8 | 服务端返回协议头无效。 | 从 2019 年 5 月开始新创建的小程序，默认强制使用 HTTPS 和 WSS 协议，不再支持 HTTP 和 WS 协议。 |
| 9 | WebSocket 请求没有指定 Sec-WebSocket-Protocol 请求头。 | 请指定 Sec-WebSocket-Protocol 请求头。 |
| 10 | 网络连接没有打开，无法发送消息。 | <ul><li><b>在未传入参数 multiple = true 时</b>，请正常连接服务器后再调用 [my.sendSocketMessage](https://opendocs.alipay.com/mini/api/mr91d1)。</li><li>发送数据消息，可通过 [my.onSocketOpen](https://opendocs.alipay.com/mini/api/itm5og) 监听事件来判断与服务器建立正确连接。</li></ul><br />**注意**：<br /><ul><li>通过 WebSocket 连接发送数据，需要先使用 [my.connectSocket](https://opendocs.alipay.com/mini/api/vx19c3) 发起连接，在 [my.onSocketOpen](https://opendocs.alipay.com/mini/api/itm5og) 回调之后再调用 [my.sendSocketMessage](https://opendocs.alipay.com/mini/api/mr91d1) 发送数据。</li><li><b>在传入参数 multiple = true 时</b>，为 WebSocket 多实例模式。可在 socketTask.onOpen() 回调中再使用 socketTask.send() 接口发送消息。</li></ul> |
| 11 | 消息发送失败。 | 稍后重试。 |
| 12 | 无法申请更多内存来读取网络数据。 | 请检查内存。 |


# 常见问题 FAQ

## Q：SocketTask 和普通的 WebSocket 使用方式有什么区别？
A：对于接口 my.connectSocket：

- 如果传入了 multiple = true，则返回一个 SocketTask 实例，本次 WebSocket 连接的所有操作（包括发送消息、接收消息、事件监听等）均在此示例上进行管理。
- 如果未传入 multiple = true 参数，则此时为默认的单实例方式，与之相关的操作请直接调用 my 上的方法。

## Q：最多支持多少个 WebSocket 实例？
A：目前最多支持 5 个 WebSocket 实例。
