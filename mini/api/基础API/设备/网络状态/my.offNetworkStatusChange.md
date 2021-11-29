
# 简介
**my.offNetworkStatusChange** 是取消监听网络状态变化的 API。

## 使用限制
此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码
```javascript
// .js
my.offNetworkStatusChange();
```

### 是否需要传 callback 值

- 不传递 callback 值，则会移除监听所有的事件监听回调。示例代码如下：
```javascript
my.offNetworkStatusChange();
```

- 传递 callback 值，只移除对应的 callback 事件。示例代码如下：
```javascript
my.offNetworkStatusChange(this.callback);
```


