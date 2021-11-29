
# 简介
**my.offBeaconUpdate** 是用于取消监听 iBeacon 设备的更新事件的 API。

## 使用限制

- 支付宝客户端 10.1.8 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 暂仅支持企业支付宝小程序使用。

# 接口调用

## 示例代码
```javascript
//.js
my.offBeaconUpdate();
```

### 是否需要传 callback 值

- 不传递 callback 值，则会移除监听所有的事件监听回调。示例代码如下：
```javascript
my.offBeaconUpdate();
```

- 传递 callback 值，只移除对应的 callback 事件。示例代码如下：
```javascript
my.offBeaconUpdate(this.callback);
```

## 入参
入参为回调函数：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| 回调函数 | Function | 取消监听 iBeacon 设备的更新事件的回调函数。 |

