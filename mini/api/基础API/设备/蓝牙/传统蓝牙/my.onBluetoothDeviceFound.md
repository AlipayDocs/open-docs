# 简介

**my.onBluetoothDeviceFound** 是搜索到新的蓝牙设备时触发的事件 API。

## 使用限制

- 支付宝客户端 10.0.18 或更高版本，若版本较低，建议采取 [兼容处理](/mini/framework/compatibility)。
- IDE 模拟器暂不支持调试，请以真机调试结果为准。
- 模拟器可能无法获取 advertisData 及 RSSI ，请使用真机调试。
- 开发者工具（IDE）和 Android 上获取到的 deviceId 为设备 MAC 地址，iOS 上则为设备 UUID。因此 deviceId 不能硬编码到代码中，需要分平台处理。iOS 可根据设备属性（localName / advertisData / manufacturerData 等）进行动态匹配。
- 若在 my.onBluetoothDeviceFound 回调中包含了某个蓝牙设备，则此设备会添加到 [my.getBluetoothDevices](https://opendocs.alipay.com/mini/api/pelizr) 接口获取到的数组中。
- 此 API 暂仅支持企业支付宝小程序使用。

# 接口调用

## 示例代码

### .acss 示例代码

```plain
/* .acss */
.help-info {
  padding:10px;
  color:#000000;
}
.help-title {
  padding:10px;
  color:#FC0D1B;
}
```

### .json 示例代码

```json
{
  "defaultTitle": "Bluetooth"
}
```

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
// .js
Page({
  data: {
    devid: '0D9C82AD-1CC0-414D-9526-119E08D28124',
    serid: 'FEE7',
    notifyId: '36F6',
    writeId: '36F5',
    charid: '',
    alldev: [{ deviceId: '' }],
  },
  //获取本机蓝牙开关状态
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
  //扫描蓝牙设备
  startBluetoothDevicesDiscovery() {
    my.startBluetoothDevicesDiscovery({
      allowDuplicatesKey: false,
      success: () => {
        my.onBluetoothDeviceFound(res => {
          var deviceArray = res.devices;
          for (var i = deviceArray.length - 1; i >= 0; i--) {
            var deviceObj = deviceArray[i];
            //通过设备名称或者广播数据匹配目标设备，然后记录deviceID后面使用
            if (deviceObj.name == this.data.name) {
              my.alert({ content: '目标设备被找到' });
              my.offBluetoothDeviceFound();
              this.setData({
                deviceId: deviceObj.deviceId,
              });
              break;
            }
          }
        });
      },
      fail: error => {
        my.alert({ content: '启动扫描失败' + JSON.stringify(error) });
      },
    });
  },
  //停止扫描
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
  //获取正在连接中的设备
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
  //获取所有搜索到的设备
  getBluetoothDevices() {
    my.getBluetoothDevices({
      success: res => {
        my.alert({ content: JSON.stringify(res) });
      },
      fail: error => {
        my.alert({ content: JSON.stringify(error) });
      },
    });
  },
  bindKeyInput(e) {
    this.setData({
      devid: e.detail.value,
    });
  },
  //连接设备
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
  //断开连接
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
  //获取连接设备的server，必须要再连接状态状态之下才能获取
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
  //获取连接设备的charid，必须要再连接状态状态之下才能获取（这里分别筛选出读写特征字）
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
            //特征字对象属性见文档，根据属性匹配读写特征字并记录，然后后面读写使用
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
  //读写数据
  readBLECharacteristicValue() {
    my.getConnectedBluetoothDevices({
      success: res => {
        if (res.devices.length === 0) {
          my.alert({ content: '没有已连接的设备' });
          return;
        }
        this.setData({
          devid: res.devices[0].deviceId,
        });
        my.readBLECharacteristicValue({
          deviceId: this.data.devid,
          serviceId: this.data.serid,
          characteristicId: this.data.notifyId,
          //1、安卓读取服务
          // serviceId:'0000180d-0000-1000-8000-00805f9b34fb',
          // characteristicId:'00002a38-0000-1000-8000-00805f9b34fb',
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
        my.writeBLECharacteristicValue({
          deviceId: this.data.devid,
          serviceId: this.data.serid,
          characteristicId: this.data.charid,
          //安卓写入服务
          //serviceId:'0000180d-0000-1000-8000-00805f9b34fb',
          //characteristicId:'00002a39-0000-1000-8000-00805f9b34fb',
          value: 'ABCD',
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
          characteristicId: this.data.notifyId,
          success: () => {
            //监听特征值变化的事件
            my.onBLECharacteristicValueChange(res => {
              my.alert({ content: '得到响应数据 = ' + res.value });
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
  offBLECharacteristicValueChange() {
    my.offBLECharacteristicValueChange();
  },
  //其他事件
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

Function 类型。callback 回调函数的入参为 Object 类型，属性如下：

| **属性** | **类型** | **描述**             |
| -------- | -------- | -------------------- |
| devices  | Array    | 新搜索到的设备列表。 |

### device 对象

| **属性**               | **类型**   | **描述**                         |
| ---------------------- | ---------- | -------------------------------- |
| name                   | String     | 蓝牙设备名称，某些设备可能没有。 |
| deviceName(兼容旧版本) | String     | 值与 name 一致。                 |
| localName              | String     | 广播设备名称。                   |
| deviceId               | String     | 设备 ID。                        |
| RSSI                   | Number     | 设备信号强度。                   |
| advertisData           | Hex String | 设备的广播内容。                 |
