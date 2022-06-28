# 简介

**my.notifyBLECharacteristicValueChange** 是启用低功耗蓝牙设备特征值变化时的 notify 功能的 API。

## 使用限制

- 支付宝客户端 10.0.18 或更高版本，若版本较低，建议采取 [兼容处理](/mini/framework/compatibility)。
- 支持 iOS 客户端，Android 5.0 及以上版本客户端。
- IDE 模拟器暂不支持调试，请以真机调试结果为准。
- 设备的特征值必须支持 notify/indicate 才可以成功调用，具体可参照 characteristic（特征值）的 [properties 属性](https://opendocs.alipay.com/mini/api/fmg9gg#success%20%E5%9B%9E%E8%B0%83%E5%87%BD%E6%95%B0)。
- 必须先启用 notify 才能监听到设备特征值变化的 notify 功能事件。
- 订阅操作成功后需要设备主动更新特征值的 value，才会触发 [my.onBLECharacteristicValueChange](https://opendocs.alipay.com/mini/api/cdu501) 。
- 订阅方式效率比较高，推荐使用订阅代替 read 方式。
- 此 API 暂仅支持企业支付宝小程序使用。

## 扫码体验

![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/558ee078cb954586bdd4588bbe85fd7a.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=stroke&width=127)

## 效果示例

![|723x407](https://gw.alipayobjects.com/zos/skylark-tools/public/files/75e9f630574f43d74e57a0cd2d2db860.png#align=left&display=inline&height=420&margin=%5Bobject%20Object%5D&originHeight=720&originWidth=1280&status=done&style=stroke&width=746)

# 接口调用

## 示例代码

完整蓝牙能力示例请见 [my.connectBLEDevice](https://opendocs.alipay.com/mini/api/tmew6e) 中的示例代码。

### .js 示例代码

```javascript
// .js
my.notifyBLECharacteristicValueChange({
  deviceId: deviceId,
  serviceId: serviceId,
  characteristicId: characteristicId,
  success: (res) => {
    console.log(res);
  },
  fail: (res) => {},
  complete: (res) => {},
});
```

## 入参

Object 类型，属性如下：

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| deviceId | String | 是 | 蓝牙设备 ID，参考 device 对象。 |
| serviceId | String | 是 | 蓝牙特征值对应 service 的 UUID。 |
| characteristicId | String | 是 | 蓝牙特征值的 UUID。 |
| descriptorId | String | 否 | notify 的 descriptor 的 UUID（Android 系统特有，默认值为 00002902-0000-10008000-00805f9b34fb）。 |
| state | Boolean | 否 | 是否启用 notify 或 indicate。<br />**注意**：此参数从支付宝客户端 10.0.20 开始支持。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |
