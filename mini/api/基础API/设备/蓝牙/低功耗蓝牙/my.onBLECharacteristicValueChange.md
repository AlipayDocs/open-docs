# 简介

**my.onBLECharacteristicValueChange** 是监听低功耗蓝牙设备的特征值变化的事件的 API。
## 使用限制

- 支付宝客户端 10.0.18 或更高版本，若版本较低，建议采取 [兼容处理](/mini/framework/compatibility)。
- 支持 iOS 客户端，Android 5.0 及以上版本客户端。
- IDE 模拟器暂不支持调试，请以真机调试结果为准。
- 使用该 API 之前需要先调用 [my.notifyBLECharacteristicValueChange](https://opendocs.alipay.com/mini/api/pdzk44) 接口才能接收到设备推送的特征值变化。
- 为防止多次事件监听导致一次事件多次回调的情况，建议每次调用 on 方法监听事件之前，先调用 off 方法，关闭之前的事件监听。
- 此 API 暂仅支持企业支付宝小程序使用。

## 扫码体验

![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/b901af23d934e7ebc5d0dea82effdd4d.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=stroke&width=127)

## 效果示例

![|723x407](https://gw.alipayobjects.com/zos/skylark-tools/public/files/d88a0c2b332da204679bd9b04bcef81f.png#align=left&display=inline&height=420&margin=%5Bobject%20Object%5D&originHeight=720&originWidth=1280&status=done&style=stroke&width=746)

# 接口调用

## 示例代码
完整蓝牙能力示例代码请见 [my.connectBLEDevice](https://opendocs.alipay.com/mini/api/tmew6e) 中的示例代码。

### .axml 示例代码

```html
<!-- .axml-->
<view class="page">
  <view class="page-description">蓝牙 API</view>
  <view class="page-section"> 
       <button type="primary" onTap="notifyBLECharacteristicValueChange">监听特征值数据变化</button>   
  </view>
</view>
```

### .js 示例代码

```javascript
// .js
Page({
  data: {
    devid: '0D9C82AD-1CC0-414D-9526-119E08D28124',
    serid: 'FEE7',
    charid:'8667556C-9A37-4C91-84ED-54EE27D90049'
  },
  onBLECharacteristicValueChange() {
    my.notifyBLECharacteristicValueChange({
      state: true,
      deviceId: this.data.devid,
      serviceId: this.data.serid,
      characteristicId: this.data.charid,
      success: () => {
        //监听特征值变化的事件
        my.onBLECharacteristicValueChange((res) => {
          my.alert({ content: '得到响应数据 = ' + res.value + res.characteristicId + res.deviceId + res.serviceId });
        });
        my.alert({ content: '监听成功' });
      },
      fail: (error) => {
        my.alert({ content: '监听失败' + JSON.stringify(error) });
      },
    });
  }
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
