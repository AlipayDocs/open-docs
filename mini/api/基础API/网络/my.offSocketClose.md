# 简介

**my.offSocketClose** 是取消监听 WebSocket 关闭事件的 API。

## 使用限制

此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

**注意**：案例仅供参考，建议使用自己的地址进行测试。

```javascript
// .js
Page({
  onLoad() {
    my.onSocketClose(this.callback);
  },
  onUnload() {
    my.offSocketClose(this.callback);
    //    my.offSocketClose();
  },
  callback(res) {
    my.alert({ content: '连接已关闭！' });
    this.setData({
      sendMessageAbility: false,
      closeLinkAbility: false,
    });
  },
});
```

### 是否需要传 callback 值

- 不传递 callback 值，则会移除监听所有的事件回调。示例代码如下：<br />

```javascript
my.offSocketClose();
```

- 传递 callback 值，只移除对应的 callback 事件。示例代码如下：<br />

```javascript
my.offSocketClose(this.callback);
```
