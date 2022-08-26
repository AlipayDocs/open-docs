# 简介

**my.offSocketOpen** 是取消监听 WebSocket 连接打开事件的 API。

## 使用限制

此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

案例仅供参考，建议使用自己的地址进行测试。

```javascript
// .js
Page({
  onLoad() {
    this.callback = this.callback.bind(this);
    my.onSocketOpen(this.callback);
  },
  onUnload() {
    my.offSocketOpen(this.callback);
  },
  callback(res) {},
});
```

### 是否需要传 callback 值

- 不传递 callback 值，则会移除监听所有的事件回调。示例代码如下：

```javascript
my.offSocketOpen();
```

- 传递 callback 值，只移除对应的 callback 事件。示例代码如下：

```javascript
my.offSocketOpen(this.callback);
```
