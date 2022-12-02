
## 通信说明
- [web-view](https://opendocs.alipay.com/mini/component/web-view) 内嵌 H5 内通过 my.postMessage 向小程序 postMessage 消息，通过 my.onMessage 接收来自小程序的消息。
- 小程序通过 onMessage 属性注册函数接收 H5 发生过来的信息，在接收到信息后可通过 this.webViewContext.postMessage 向 H5 发送 postMessage 消息。
- 支持 web-view 的 postMessage 传递多个参数。

**注意**：双向通信能力的流程是 H5 先发消息给小程序，小程序接收到消息后再发消息给 H5。

## 示例代码
web-view H5 页面代码：
```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <title>webview与小程序通信</title>
</head>

<body>
  <button onclick="send()">发送</button>
  <button onclick="isminiapp()">判断是否在小程序内</button>
  <button onclick="onmessage()">开始监听小程序发送的消息</button>
  <button onclick="getminiappid()">我要调用小程序获取APPID的API</button>
  <!-- h5 log 工具方便在小程序内查看h5的log-->
  <script src="https://cdn.jsdelivr.net/npm/eruda"></script>
  <script>
    eruda.init();
  </script>
  <!--引入https://appx/web-view.min.js， 如该 H5 页面需要同时在非支付宝客户端内使用，为避免该请求404，可参考以下写法 -->
  <script>
    if (navigator.userAgent.indexOf('AlipayClient') > -1) {
      document.writeln('<script src="https://appx/web-view.min.js"' + '>' + '<' + '/' + 'script>');
    }
  </script>
  <script>
    //发送消息
    function send() {
      my.postMessage({
        name: "h5发送测试web-view"
      });
    }
    //监听小程序发给H5页面的消息
    function onmessage() {
      my.onMessage = function (e) {
        console.log(e);
      }
    }
    //判断是否在小程序内
    function isminiapp() {
      my.getEnv(function (res) {
        console.log(res.miniprogram) // true  
      });
    }
    //H5内通过通信获取APPID（先给小程序发送消息，表示H5内需要APPID）
    function getminiappid() {
      my.postMessage({
        name: "getappid"
      });
    }
  </script>
</body>
  
</html>
```
 my.postMessage 信息发送后，小程序页面接收信息时，会执行 onMessage 配置的方法：
```xml
<!--axml-->
<!--网址后面拼接一个随机参数是为了避免html缓存问题-->
<web-view id="web-view-1" src="http://30.5.70.34:5000/static/html/test.html?a={{a}}" onMessage="onmessage" />
```
```javascript
// 小程序页面对应的 page.js 声明 onmessage方法，
// 由于 page.axml 里的 web-view 组件设置了 onMessage="onmessage",
// 当页面里执行完 my.postMessage 后，onmessage 方法会被执行
//js
Page({ 
    data: { 
      a: Math.floor(Math.random() * 100) + 1  },
    onLoad(e) {
    //初始化webViewContext    
    this.webViewContext = my.createWebViewContext('web-view-1');
  },  
  //监听来自于H5页面的消息  
  onmessage(e) {
    console.log('收到消息', e.detail.name)   //根据name判断是什么消息  
    if (e.detail.name == 'getappid') {    //将处理结果通过消息发送给H5页面
      this.webViewContext.postMessage({ 'getappid': my.getAppIdSync() });
    }  
  }});
```
 <br /> <br /> 
