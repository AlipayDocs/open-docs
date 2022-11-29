# 简介

**my.connectBLEDevice** 是连接低功耗蓝牙设备的 API。

## 使用限制

- 支付宝客户端 10.0.18 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 支持 iOS 客户端，Android 5.0 及以上版本客户端。
- IDE 模拟器暂不支持调试，请以真机调试结果为准。
- 若小程序在之前已搜索过某个蓝牙设备，即可直接传入之前搜索获取的 deviceId 尝试连接该设备，无需进行搜索操作。
- 若指定的蓝牙设备已连接，重复连接将直接返回 success。
- 此 API 暂仅支持企业支付宝小程序使用。

## 扫码体验

![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/877a849ee8634d8baf83ca2342a44095.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=stroke&width=127)

## 效果示例

![|723x407](https://gw.alipayobjects.com/zos/skylark-tools/public/files/0776214e9b859e4c167eb9051086d99d.png#align=left&display=inline&height=420&margin=%5Bobject%20Object%5D&originHeight=720&originWidth=1280&status=done&style=stroke&width=746)

# 接口调用

## 示例代码

### .axml 示例代码

```html
<!-- .axml-->
<view class="page">
  <view class="page-description">蓝牙 API</view>
  <view class="page-section">
    <view class="page-section-title">本机蓝牙开关状态</view>
    <view class="page-section-demo">
      <button type="primary" onTap="openBluetoothAdapter">初始化蓝牙</button>
      <button type="primary" onTap="closeBluetoothAdapter">关闭本机蓝牙</button>
      <button type="primary" onTap="getBluetoothAdapterState">获取蓝牙状态</button>
    </view>

    <view class="page-section-title">扫描蓝牙设备</view>
    <view class="page-section-demo">
      <button type="primary" onTap="startBluetoothDevicesDiscovery">开始搜索</button>
      <button type="primary" onTap="getBluetoothDevices">所有搜索到的设备</button>
      <button type="primary" onTap="getConnectedBluetoothDevices">所有已连接的设备</button>
      <button type="primary" onTap="stopBluetoothDevicesDiscovery">停止搜索</button>
    </view>

    <view class="page-section-title">连接设备</view>
    <view class="page-section-demo">
      <input class="input" onInput="bindKeyInput" type="{{text}}" placeholder="输入要连接的设备的deviceId"></input>
      <button type="primary" onTap="connectBLEDevice">连接设备</button>
      <button type="primary" onTap="getBLEDeviceServices">获取设备服务</button>
      <button type="primary" onTap="getBLEDeviceCharacteristics">获取读写特征</button>
      <button type="primary" onTap="disconnectBLEDevice">断开设备连接</button>
    </view>

    <view class="page-section-title">读写数据</view>
    <view>
      <text>
        charid: {{charid}} \n
      </text>
      <text>
        devid: {{devid}} \n
      </text>
      <text>
        serid: {{serid}} \n
      </text>
    </view>
    <view class="page-section-demo">
      <button type="primary" onTap="notifyBLECharacteristicValueChange">监听特征值数据变化</button>
      <button type="primary" onTap="readBLECharacteristicValue">读取数据</button>
      <button type="primary" onTap="writeBLECharacteristicValue">写入数据</button>
      <button type="primary" onTap="offBLECharacteristicValueChange">取消特征值监听</button>
    </view>

    <view class="page-section-title">其他事件</view>
    <view class="page-section-demo">
      <button type="primary" onTap="bluetoothAdapterStateChange">本机蓝牙状态变化</button>
      <button type="primary" onTap="offBluetoothAdapterStateChange">取消本机蓝牙状态监听</button>
      <button type="primary" onTap="BLEConnectionStateChanged">蓝牙连接状态变化</button>
      <button type="primary" onTap="offBLEConnectionStateChanged">取消蓝牙连接状态监听</button>
    </view>
  </view>
</view>
```

### .js 示例代码

```javascript
Page({
  data: {
    devid: '',
    serid: '',
    writeId: '',
    charid: '',
  },
  // 获取本机蓝牙开关状态
  openBluetoothAdapter() {
    my.openBluetoothAdapter({
      success: res => {
        if (!res.isSupportBLE) {
          my.alert({ content: '抱歉，您的手机蓝牙暂不可用' });
          return;
        }
        my.alert({ content: '初始化成功！' });
      },
      fail: error => {
        my.alert({ content: JSON.stringify(error) });
      },
    });
  },
  // 关闭蓝牙
  closeBluetoothAdapter() {
    my.closeBluetoothAdapter({
      success: () => {
        my.alert({ content: '关闭蓝牙成功！' });
      },
      fail: error => {
        my.alert({ content: JSON.stringify(error) });
      },
    });
  },
  // 获取本机蓝牙状态
  getBluetoothAdapterState() {
    my.getBluetoothAdapterState({
      success: res => {
        if (!res.available) {
          my.alert({ content: '抱歉，您的手机蓝牙暂不可用' });
          return;
        }
        my.alert({ content: JSON.stringify(res) });
      },
      fail: error => {
        my.alert({ content: JSON.stringify(error) });
      },
    });
  },
  // 扫描蓝牙设备
  startBluetoothDevicesDiscovery() {
    my.startBluetoothDevicesDiscovery({
      allowDuplicatesKey: false,
      success: () => {
        my.onBluetoothDeviceFound({
          success: res => {
            // my.alert({content:'监听新设备'+JSON.stringify(res)});
            var deviceArray = res.devices;
            for (var i = deviceArray.length - 1; i >= 0; i--) {
              var deviceObj = deviceArray[i];
              // 通过设备名称或者广播数据匹配目标设备，然后记录 deviceID 后面使用
              if (deviceObj.name == this.data.name) {
                my.alert({ content: '目标设备被找到' });
                my.offBluetoothDeviceFound();
                this.setData({
                  deviceId: deviceObj.deviceId,
                });
                break;
              }
            }
          },
          fail: error => {
            my.alert({ content: '监听新设备失败' + JSON.stringify(error) });
          },
        });
      },
      fail: error => {
        my.alert({ content: '启动扫描失败' + JSON.stringify(error) });
      },
    });
  },
  // 停止扫描
  stopBluetoothDevicesDiscovery() {
    my.stopBluetoothDevicesDiscovery({
      success: res => {
        my.offBluetoothDeviceFound();
        my.alert({ content: '操作成功！' });
      },
      fail: error => {
        my.alert({ content: JSON.stringify(error) });
      },
    });
  },
  // 获取正在连接中的设备
  getConnectedBluetoothDevices() {
    my.getConnectedBluetoothDevices({
      success: res => {
        if (res.devices.length === 0) {
          my.alert({ content: '没有在连接中的设备！' });
          return;
        }
        my.alert({ content: JSON.stringify(res) });
        this.setData({
          devid: res.devices[0].deviceId,
        });
      },
      fail: error => {
        my.alert({ content: JSON.stringify(error) });
      },
    });
  },
  // 获取所有搜索到的设备
  getBluetoothDevices() {
    my.getBluetoothDevices({
      success: res => {
        console.log('getBluetoothDevices', JSON.stringify(res));
        console.log('getBluetoothDevices', res);
        my.alert({ content: JSON.stringify(res) });
      },
      fail: error => {
        my.alert({ content: JSON.stringify(error) });
      },
    });
  },
 // "输入要连接的设备的 deviceId" Input 框事件
  bindKeyInput(e) {
    this.setData({
      devid: e.detail.value,
    });
  },
  // 连接设备
  connectBLEDevice() {
    my.connectBLEDevice({
      deviceId: this.data.devid,
      success: res => {
        my.alert({ content: '连接成功' });
      },
      fail: error => {
        my.alert({ content: JSON.stringify(error) });
      },
    });
  },
  // 断开连接
  disconnectBLEDevice() {
    my.disconnectBLEDevice({
      deviceId: this.data.devid,
      success: () => {
        my.alert({ content: '断开连接成功！' });
      },
      fail: error => {
        my.alert({ content: JSON.stringify(error) });
      },
    });
  },
  // 获取连接设备的 server，必须要再连接状态状态之下才能获取
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
  // 获取连接设备的 charid，必须要再连接状态状态之下才能获取（这里分别筛选出读写特征字）
  getBLEDeviceCharacteristics() {
    my.getConnectedBluetoothDevices({
      success: res => {
        if (res.devices.length === 0) {
          my.alert({ content: '没有已连接的设备' });
          return;
        }
        this.setData({
          devid: res.devices[0].deviceId,
        });
        my.getBLEDeviceCharacteristics({
          deviceId: this.data.devid,
          serviceId: this.data.serid,
          success: res => {
            my.alert({ content: JSON.stringify(res) });
            // 特征字对象属性见文档，根据属性匹配读写特征字并记录，然后后面读写使用
            this.setData({
              charid: res.characteristics[0].characteristicId,
            });
          },
          fail: error => {
            my.alert({ content: JSON.stringify(error) });
          },
        });
      },
    });
  },
  // 读数据
  readBLECharacteristicValue() {
    my.getConnectedBluetoothDevices({
      success: res => {
        if (res.devices.length === 0) {
          my.alert({ content: '没有已连接的设备' });
          return;
        }
        my.alert({
          title: '使用的设备',
          content: JSON.stringify(res.devices[0]),
        });
        this.setData({
          devid: res.devices[0].deviceId,
        });
        my.readBLECharacteristicValue({
          deviceId: this.data.devid,
          serviceId: this.data.serid,
          characteristicId: this.data.charid,
          success: res => {
            my.alert({ content: JSON.stringify(res) });
          },
          fail: error => {
            my.alert({ content: '读取失败' + JSON.stringify(error) });
          },
        });
      },
    });
  },
  // 写数据
  writeBLECharacteristicValue() {
    my.getConnectedBluetoothDevices({
      success: res => {
        if (res.devices.length === 0) {
          my.alert({ content: '没有已连接的设备' });
          return;
        }
        this.setData({
          devid: res.devices[0].deviceId,
        });
        // 向蓝牙设备发送一个 0x00 的 16 进制数据
        const buffer = new ArrayBuffer(1);
        const dataView = new DataView(buffer);
        dataView.setUint8(0, 0);
        my.writeBLECharacteristicValue({
          deviceId: this.data.devid,
          serviceId: this.data.serid,
          characteristicId: this.data.charid,
          value: buffer,
          success: res => {
            my.alert({ content: '写入数据成功！' });
          },
          fail: error => {
            my.alert({ content: JSON.stringify(error) });
          },
        });
      },
    });
  },
  // 监听特征值变化的事件
  notifyBLECharacteristicValueChange() {
    my.getConnectedBluetoothDevices({
      success: res => {
        if (res.devices.length === 0) {
          my.alert({ content: '没有已连接的设备' });
          return;
        }
        this.setData({
          devid: res.devices[0].deviceId,
        });

        my.notifyBLECharacteristicValueChange({
          state: true,
          deviceId: this.data.devid,
          serviceId: this.data.serid,
          characteristicId: this.data.charid,
          success: () => {
            // 监听特征值变化的事件
            my.onBLECharacteristicValueChange({
              success: res => {
                //  my.alert({content: '特征值变化：'+JSON.stringify(res)});
                my.alert({ content: '得到响应数据 = ' + res.value });
              },
            });
            my.alert({ content: '监听成功' });
          },
          fail: error => {
            my.alert({ content: '监听失败' + JSON.stringify(error) });
          },
        });
      },
    });
  },
  // 取消监听低功耗蓝牙设备的特征值变化
  offBLECharacteristicValueChange() {
    my.offBLECharacteristicValueChange();
  },
  // 监听本机蓝牙状态变化
  bluetoothAdapterStateChange() {
    my.onBluetoothAdapterStateChange(
      this.getBind('onBluetoothAdapterStateChange')
    );
  },
  onBluetoothAdapterStateChange(res) {
    if (res.error) {
      my.alert({ content: JSON.stringify(res.error) });
    } else {
      my.alert({ content: '本机蓝牙状态变化：' + JSON.stringify(res) });
    }
  },
  offBluetoothAdapterStateChange() {
    my.offBluetoothAdapterStateChange(
      this.getBind('onBluetoothAdapterStateChange')
    );
  },
  getBind(name) {
    if (!this[`bind${name}`]) {
      this[`bind${name}`] = this[name].bind(this);
    }
    return this[`bind${name}`];
  },
  // 监听低功耗蓝牙连接的错误事件
  BLEConnectionStateChanged() {
    my.onBLEConnectionStateChanged(this.getBind('onBLEConnectionStateChanged'));
  },
  onBLEConnectionStateChanged(res) {
    if (res.error) {
      my.alert({ content: JSON.stringify(res.error) });
    } else {
      my.alert({ content: '连接状态变化：' + JSON.stringify(res) });
    }
  },
  // 取消监听低功耗蓝牙连接状态变化
  offBLEConnectionStateChanged() {
    my.offBLEConnectionStateChanged(
      this.getBind('onBLEConnectionStateChanged')
    );
  },
  onUnload() {
    this.offBLEConnectionStateChanged();
    this.offBLECharacteristicValueChange();
    this.offBluetoothAdapterStateChange();
    this.closeBluetoothAdapter();
  },
});
```

## 入参

Object 类型，属性如下：

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| deviceId | String | 是 | 蓝牙设备 ID。Android 上为设备 MAC 地址，iOS 上为设备 UUID。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

## 错误码

| **错误码** | **说明**                   | **解决方案**               |
| ---------- | -------------------------- | -------------------------- |
| 1          | 在 IDE 中调用了此 API。    | 请在真机中调试。 |
| 12         | 蓝牙未打开。               | 请尝试打开系统设置中的蓝牙开关。           |
| 13         | 与系统服务的链接暂时丢失。 | 请尝试重新连接。           |
| 2001       | 用户不允许授权。                 | 请授权当前小程序使用蓝牙功能。|
| 2002       | 用户不允许授权，且勾选了“总是保持以上选择，不再询问“后，再次调用该接口。                | 请授权当前小程序使用蓝牙功能。|
| 2003       | 用户不允许授权，且勾选了“总是保持以上选择，不再询问”。 | 请授权当前小程序使用蓝牙功能。|


# 常见问题 FAQ

## Q：如果系统权限未开启，接口调用报错，如何引导开启系统权限？

A：可以调用 [my.showAuthGuide](https://opendocs.alipay.com/mini/api/show-auth-guide) 引导用户开启相关系统权限。
