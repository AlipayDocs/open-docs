# 简介

**my.getBLEDeviceServices** 是获取指定低功耗蓝牙设备所有服务列表的 API。

## 使用限制

- 支付宝客户端 10.0.18 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 支持 iOS 客户端，Android 5.0 及以上版本客户端。
- IDE 模拟器暂不支持调试，请以真机调试结果为准。
- 此 API 暂仅支持企业支付宝小程序使用。

## 扫码体验

![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/b78436ea1396f5bbcd702cd8db77186d.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=none&width=127)

## 效果示例

![|723x407](https://gw.alipayobjects.com/zos/skylark-tools/public/files/6fafc6048769544f55190149f0f55ab0.png#align=left&display=inline&height=420&margin=%5Bobject%20Object%5D&originHeight=720&originWidth=1280&status=done&style=none&width=746)

# 接口调用

## 示例代码

完整蓝牙能力示例请见 [my.connectBLEDevice](https://opendocs.alipay.com/mini/api/tmew6e) 中的示例代码。

### .js 示例代码

```javascript
// .js
//获取连接设备的server，必须要在连接状态之下才能获取
  getBLEDeviceServices() {
    my.getConnectedBluetoothDevices({
      success: res => {
        if (res.devices.length === 0) {
          my.alert({ content: '没有已连接的设备' });
          return;
        }
        my.getBLEDeviceServices({
          deviceId: this.data.devid,
          success: res => {
            my.alert({ content: JSON.stringify(res) });
            this.setData({
              serid: res.services[0].serviceId,
            });
          },
          fail: error => {
            my.alert({ content: JSON.stringify(error) });
          },
        });
      },
    });
  },
```

## 返回示例

### success 回调返回示例

执行成功时，触发 success 回调，回调参数示例如下：

```json
{
  "services": [
    {
      "isPrimary": true,
      "serviceId": "00001800-0000-1000-8000-00805f9b34fb"
    },
    {
      "isPrimary": true,
      "serviceId": "00001801-0000-1000-8000-00805f9b34fb"
    },
    {
      "isPrimary": true,
      "serviceId": "d0611e78-bbb4-4591-a5f8-487910ae4366"
    },
    {
      "isPrimary": true,
      "serviceId": "9fa480e0-4967-4542-9390-d343dc5d04ae"
    }
  ]
}
```

## 入参

Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| deviceId | String | 是 | 蓝牙设备 ID。Android 上为设备 MAC 地址，iOS 上为设备 UUID。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

### Function success

success 回调函数会携带一个 Object 类型的对象，其属性如下：

| **属性** | **类型** | **描述**               |
| -------- | -------- | ---------------------- |
| services | Array    | 已发现的设备服务列表。 |

#### Array services

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| isPrimary | Boolean | 该服务是否为主服务。<ul><li> `true` 为主服务。</li><li>`false` 不是主服务。</li></ul> |
| serviceId | String | 蓝牙设备特征值对应服务的 [UUID](https://opendocs.alipay.com/mini/developer/dhu9gf#UUID)。 |

## 错误码

| **错误码** | **说明** | **解决方案** |
| --- | --- | --- |
| 1          | IDE 不支持调用该 API。   | 请在真机上调用。           |
| 12         | 蓝牙未打开。             | 请尝试打开蓝牙。           |
| 13         | 与系统服务的连接暂时丢失。 | 请尝试重新连接。           |

