# 简介

**my.offBLECharacteristicValueChange** 是取消监听低功耗蓝牙设备的特征值变化的事件的 API。

## 使用限制

- 支付宝客户端 10.0.18 或更高版本，若版本较低，建议采取 [兼容处理](/mini/framework/compatibility)。
- 支持 iOS 客户端，Android 5.0 及以上版本客户端。
- IDE 模拟器暂不支持调试，请以真机调试结果为准。
- 此 API 暂仅支持企业支付宝小程序使用。

## 扫码体验

![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/d9e0d67c37832e1b77137b7d1e8ba64f.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=stroke&width=127)

## 效果示例

![|723x407](https://gw.alipayobjects.com/zos/skylark-tools/public/files/ef65ff73bb7264832e4ba3af9c980dd6.png#align=left&display=inline&height=420&margin=%5Bobject%20Object%5D&originHeight=720&originWidth=1280&status=done&style=stroke&width=746)

# 接口调用

## 示例代码

完整蓝牙能力示例请见 [my.connectBLEDevice](https://opendocs.alipay.com/mini/api/tmew6e) 中的示例代码。

```javascript
// .js
Page({
  onLoad() {
    this.callback = this.callback.bind(this);
    my.onBLECharacteristicValueChange(this.callback);
  },
  onUnload() {
    my.offBLECharacteristicValueChange(this.callback);
  },
  callback(res) {
    console.log(res);
  },
});
```

## 入参

Function 类型。callback 回调函数入参为 Object 类型，属性如下：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| deviceId | String | 蓝牙设备 ID。Android 上为设备 MAC 地址，iOS 上为设备 UUID。 |
| serviceId | String | 蓝牙特征值对应 service 的 UUID。 |
| characteristicId | String | 蓝牙特征值的 UUID。 |
| value | Hex String | 特征值最新的 16 进制值。 |

### 是否传递 callback 值示例

- 不传递 callback 值，则会移除监听所有的事件监听回调。示例代码如下：

```javascript
my.offBLECharacteristicValueChange();
```

- 传递 callback 值，只移除对应的 callback 事件。示例代码如下：

```javascript
my.offBLECharacteristicValueChange(this.callback);
```
