
# 简介
**my.offBluetoothDeviceFound** 是移除寻找到新的蓝牙设备事件监听的 API。

## 使用限制

- 支付宝客户端 10.0.18 或更高版本，若版本较低，建议采取 [兼容处理](/mini/framework/compatibility)。
- IDE 模拟器暂不支持调试，请以真机调试结果为准。
- 为防止多次事件监听导致一次事件多次回调的情况，建议每次调用 on 方法监听事件之前，先调用 off 方法，关闭之前的事件监听。
- 此 API 暂仅支持企业支付宝小程序使用。

# 接口调用

## 示例代码
```javascript
// .js
my.offBluetoothDeviceFound();
```

### 是否需要传 callback 值

- 不传递 callback 值，则会移除监听所有的事件监听回调。示例代码如下：
```javascript
my.offBluetoothDeviceFound();
```

- 传递 callback 值，只移除对应的 callback 事件。示例代码如下：
```javascript
my.offBluetoothDeviceFound(this.callback);
```
