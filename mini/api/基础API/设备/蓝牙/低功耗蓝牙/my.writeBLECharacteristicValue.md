
# 简介
**my.writeBLECharacteristicValue** 是向低功耗蓝牙设备特征值中写入数据的 API。

## 使用限制

- 支付宝客户端 10.0.18 或更高版本，若版本较低，建议采取 [兼容处理](/mini/framework/compatibility)。
- 支持 iOS 客户端，Android 5.0 及以上版本客户端。
- IDE 模拟器暂不支持调试，请以真机调试结果为准。
- 设备的特征值必须支持 write 才可以成功调用，具体请参见 [my.getBLEDeviceCharacteristics](https://opendocs.alipay.com/mini/api/fmg9gg) 中特征值的 properties 属性。
- 写入的二进制数据需要进行 Hex 编码。
- 此 API 暂仅支持企业支付宝小程序使用。

## 扫码体验
![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/8aae99376efa68fe095baa0df0d8b5ed.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=stroke&width=127)

## 效果示例
![|723x407](https://gw.alipayobjects.com/zos/skylark-tools/public/files/a1cbb9495099802ce89177102af3138f.png#align=left&display=inline&height=420&margin=%5Bobject%20Object%5D&originHeight=720&originWidth=1280&status=done&style=stroke&width=746)

# 接口调用

## 示例代码
```javascript
// .js
my.writeBLECharacteristicValue({
  deviceId: deviceId,
  serviceId: serviceId,
  characteristicId: characteristicId,
  value: 'fffe',
  success: (res) => {
    console.log(res)
  },
  fail:(res) => {
  },
  complete: (res)=>{
  }
});
```

## 入参
Object 类型，属性如下：

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| deviceId | String | 是 | 蓝牙设备 ID，参考 device 对象。 |
| serviceId | String | 是 | 蓝牙特征值对应 service 的 UUID。 |
| characteristicId | String | 是 | 蓝牙特征值的 UUID。 |
| value | Hex String | 是 | 蓝牙设备特征值对应的值，为 16 进制字符串，限制在 20 字节内。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

