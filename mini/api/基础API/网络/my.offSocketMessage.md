
# 简介
**my.offSocketMessage** 是取消监听 WebSocket 接收到服务器的消息事件的 API。

## 使用限制
此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码
**注意**：案例仅供参考，建议使用自己的地址进行测试。
```javascript
// .js
my.connectSocket({
  url: '服务器地址'
})
my.onSocketMessage(function(res) {
  console.log('收到服务器内容：' + res.data)
})
my.offSocketMessage();
```

### 是否需要传 callback 值

- 不传递 callback 值，则会移除监听所有的事件回调。示例代码如下：

```javascript
my.offSocketMessage();
```

- 传递 callback 值，只移除对应的 callback 事件。示例代码如下：

```javascript
my.offSocketMessage(this.callback);
```
