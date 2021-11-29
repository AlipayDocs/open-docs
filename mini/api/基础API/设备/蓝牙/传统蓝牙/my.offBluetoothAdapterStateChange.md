
# 简介
**my.offBluetoothAdapterStateChange** 是移除本机蓝牙状态变化的事件监听的 API。

## 使用限制

- 支付宝客户端 10.0.18 或更高版本，若版本较低，建议采取 [兼容处理](/mini/framework/compatibility)。
- IDE 模拟器暂不支持调试，请以真机调试结果为准。
- 为防止多次事件监听导致一次事件多次回调的情况，建议每次调用 on 方法监听事件之前，先调用 off 方法，关闭之前的事件监听。
- 此 API 暂仅支持企业支付宝小程序使用。

## 扫码体验
![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/a5079929ade4b63ffb286d38a938cb44.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=stroke&width=127)

## 效果示例
![|723x407](https://gw.alipayobjects.com/zos/skylark-tools/public/files/7b449e9e9aef112de7654e7c420b0c5a.png#align=left&display=inline&height=420&margin=%5Bobject%20Object%5D&originHeight=720&originWidth=1280&status=done&style=stroke&width=746)

# 接口调用

## 示例代码
```javascript
// .js
my.offBluetoothAdapterStateChange();
```

### 是否需要传 callback 值

- 不传递 callback 值，则会移除监听所有的事件监听回调。示例代码如下：
```javascript
my.offBluetoothAdapterStateChange();
```

- 传递 callback 值，只移除对应的 callback 事件。示例代码如下：
```javascript
my.offBluetoothAdapterStateChange(this.callback);
```
