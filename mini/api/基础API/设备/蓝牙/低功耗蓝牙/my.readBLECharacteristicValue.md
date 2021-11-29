
# 简介
**my.readBLECharacteristicValue** 是读取低功耗蓝牙设备特征值中的数据的 API。调用后在 [my.onBLECharacteristicValueChange](https://opendocs.alipay.com/mini/api/cdu501) 事件中接收数据返回。

## 使用限制

- 支付宝客户端 10.0.18 或更高版本，若版本较低，建议采取 [兼容处理](/mini/framework/compatibility)。
- 支持 iOS 客户端，Android 5.0 及以上版本客户端。
- IDE 模拟器暂不支持调试，请以真机调试结果为准。
- 设备的特征值必须支持 read 才可以成功调用，具体请参见  [my.getBLEDeviceCharacteristics](https://opendocs.alipay.com/mini/api/fmg9gg) 中特征值的 properties 属性。
- 并行多次调用读写接口存在读写失败的可能性。
- 如果读取超时，错误码为 10015，错误码信息及解决方案请参见 [蓝牙 API 错误码对照表](https://opendocs.alipay.com/mini/api/ucd2lh)。[my.onBLECharacteristicValueChange](https://opendocs.alipay.com/mini/api/cdu501) 接口之后可能返回数据，需要接入方酌情处理。 
- 此 API 暂仅支持企业支付宝小程序使用。

## 扫码体验
![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/a35b07d7b469e80e944fa14b143ce70d.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=stroke&width=127)

## 效果示例
![|723x407](https://gw.alipayobjects.com/zos/skylark-tools/public/files/e3b9acfa1fc42f82d496e4fd80095db2.png#align=left&display=inline&height=420&margin=%5Bobject%20Object%5D&originHeight=720&originWidth=1280&status=done&style=stroke&width=746)

# 接口调用

## 示例代码
```javascript
// .js
my.readBLECharacteristicValue({
  deviceId: deviceId,
  serviceId: serviceId,
  characteristicId: characteristicId,
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
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |


### success 回调函数
入参为 Object 类型，属性如下：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| characteristic | Object | 设备特征值信息。 |


### characteristic 对象
蓝牙设备 characteristic（特征值）信息。

| **名称** | **类型** | **描述** |
| --- | --- | --- |
| characteristicId | String | 蓝牙设备特征值的 UUID。 |
| serviceId | String | 蓝牙设备特征值对应服务的 UUID。 |
| value | Hex String | 蓝牙设备特征值的 value。 |

