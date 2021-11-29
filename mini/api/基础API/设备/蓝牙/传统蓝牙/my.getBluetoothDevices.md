
# 简介
**my.getBluetoothDevices** 是获取所有已发现的蓝牙设备的 API，包括已经和本机处于连接状态的设备。

## 使用限制

- 支付宝客户端 10.0.18 或更高版本，若版本较低，建议采取 [兼容处理](/mini/framework/compatibility)。
- IDE 模拟器暂不支持调试，请以真机调试结果为准。
- 模拟器可能无法获取 advertisData 及 RSSI，请使用真机调试。
- 开发者工具（IDE）和 Android 上获取到的 deviceId 为设备 MAC 地址，iOS 上则为设备 UUID；因此 deviceId 不能硬编码到代码中，需要分平台处理，iOS 可根据设备属性（ localName / advertisData / manufacturerData 等属性）进行动态匹配。
- 此 API 暂仅支持企业支付宝小程序使用。

## 扫码体验
![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/ab33cf1b17326739dc8818043221f0e9.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=stroke&width=127)

## 效果示例
![|723x407](https://gw.alipayobjects.com/zos/skylark-tools/public/files/5b9e1c045d09dd9f641655bb70f317ec.png#align=left&display=inline&height=420&margin=%5Bobject%20Object%5D&originHeight=720&originWidth=1280&status=done&style=stroke&width=746)

# 接口调用

## 示例代码
```javascript
// .js
my.getBluetoothDevices({
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
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |


### success 回调函数
入参为 Object 类型，属性如下：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| devices | Array | 已发现的设备列表。 |


### device 对象
| **属性** | **类型** | **描述** |
| --- | --- | --- |
| name | String | 蓝牙设备名称（某些设备可能没有）。 |
| deviceName(兼容旧版本) | String | 值与 name 一致。 |
| localName | String | 广播设备名称。 |
| deviceId | String | 设备 ID。 |
| RSSI | Number | 设备信号强度。 |
| advertisData | Hex String | 设备的广播内容。 |
| manufacturerData | Hex String | 设备的 manufacturerData。 |

