# 简介

**my.writeBLECharacteristicValue** 是向低功耗蓝牙设备特征值中写入数据的 API。

## 使用限制

- 支付宝客户端 10.0.18  或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 支持 iOS 客户端，Android 5.0 及以上版本客户端。
- IDE 模拟器暂不支持调试，请以真机调试结果为准。
- 设备的特征值必须支持 write 才可以成功调用，具体可查看 [my.getBLEDeviceCharacteristics](https://opendocs.alipay.com/mini/api/fmg9gg) 中特征值的 properties 属性。
- 写入的二进制数据需要进行 Hex 编码。
- 此 API 暂仅支持企业支付宝小程序使用。

## 扫码体验

![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/8aae99376efa68fe095baa0df0d8b5ed.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=stroke&width=127)

## 效果示例

![|723x407](https://gw.alipayobjects.com/zos/skylark-tools/public/files/a1cbb9495099802ce89177102af3138f.png#align=left&display=inline&height=420&margin=%5Bobject%20Object%5D&originHeight=720&originWidth=1280&status=done&style=stroke&width=746)

# 接口调用

## 示例代码

完整蓝牙能力示例请见 [my.connectBLEDevice](https://opendocs.alipay.com/mini/api/tmew6e) 中的示例代码。

### .js 示例代码

```javascript
// .js
// 向蓝牙设备发送一个 0x00 的 16 进制数据
const buffer = new ArrayBuffer(1);
const dataView = new DataView(buffer);
dataView.setUint8(0, 0);

my.writeBLECharacteristicValue({
  deviceId: deviceId,
  serviceId: serviceId,
  characteristicId: characteristicId,
  value: buffer,
  success: (res) => {
    console.log(res);
  },
  fail: (res) => {},
  complete: (res) => {},
});
```

## 入参

Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| deviceId | String | 是 | 蓝牙设备 ID。Android 上为设备 MAC 地址，iOS 上为设备 UUID。 |
| serviceId | String | 是 | 蓝牙特征值对应 service 的 UUID。 |
| characteristicId | String | 是 | 蓝牙特征值的 UUID。 |
| value | ArrayBuffer \| Hex String | 是 | 蓝牙设备特征值对应的二进制值，需要转为 ArrayBuffer 或 16 进制字符串。小程序不会对写入数据包大小做限制，但系统与蓝牙设备会限制蓝牙 4.0 单次传输的数据大小，超过最大字节数后会发生写入错误，建议每次写入不超过 20 字节。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

# 常见问题 FAQ

## 如何获取写入的结果？如何确定写入是否成功？

该 API 的 success 回调的第一个参数是不带写入的数据的，仅代表向设备发送该请求成功。

可以通过调用 [`my.notifyBLECharacteristicValueChange`](https://opendocs.alipay.com/mini/api/pdzk44) 激活设备上的主动通知(请注意，这需要你的设备支持 notify，详情请查看该文档)。然后使用 [`my.onBLECharacteristicValueChange`](https://opendocs.alipay.com/mini/api/cdu501) 来监听设备上值的变化。可以通过 [`my.offBLECharacteristicValueChange`](https://opendocs.alipay.com/mini/api/dlxobk) 来取消监听。

此外，主动调用 [`my.readBLECharacteristicValue`](https://opendocs.alipay.com/mini/api/zro0ka) 也可以在 [`my.onBLECharacteristicValueChange`](https://opendocs.alipay.com/mini/api/cdu501) 中接收数据返回。

## 小程序发送写入请求成功后机器没有收到写入值？

请按以下步骤进行排查：

1. 请检查入参中的 `deviceId` 是否正确，是否连接到了正确的设备。
2. 请检查入参中的 `serviceId` 是否正确，是否设置了正确的 id。
3. 请检查入参中的 `characteristicId` 是否正确，是否设置了正确的 id。
