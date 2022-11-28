# 简介

**my.openBluetoothAdapter** 是初始化小程序蓝牙模块的 API。经过初始化后的小程序蓝牙模块的生命周期为：调用 my.openBluetoothAdapter 至调用 [my.closeBluetoothAdapter](https://opendocs.alipay.com/mini/api/wvko0w) 或 小程序被销毁为止。

在小程序蓝牙适配器模块生效期间，开发者可以正常调用开发链路流程中其他的小程序 API，（具体开发链路流程可查看[蓝牙 API 概览](https://opendocs.alipay.com/mini/api/bluetooth-intro)中的流程图），并会收到蓝牙模块相关的 on 事件回调。

## 使用限制

- 支付宝客户端 10.0.18 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- IDE 模拟器暂不支持调试，请以真机调试结果为准。如果在 IDE 上调用该 API 会进入 fail 回调，并且返回 "error":1 的错误码。
- 在调用 my.openBluetoothAdapterAPI 之前，调用小程序其它蓝牙模块相关 API，API 会返回错误。
  - 错误码：10000。
  - 错误描述：未初始化蓝牙适配器。
  - 解决方案：请调用 my.openBluetoothAdapter。
- 在用户蓝牙开关未开启或者手机不支持蓝牙功能的情况下，调用 my.openBluetoothAdapter 会返回错误。错误码详情请参见 [蓝牙 API 错误码对照表](https://opendocs.alipay.com/mini/api/ucd2lh)；当小程序蓝牙模块已经初始化完成，可通过 [my.onBluetoothAdapterStateChange](https://opendocs.alipay.com/mini/api/eegfbk) 监听手机蓝牙状态的改变。
- 此 API 暂仅支持企业支付宝小程序使用。

## 扫码体验

![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/7c724fcc6736c7411a95f7a2850300a6.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=stroke&width=127)

## 效果示例

![|723x407](https://gw.alipayobjects.com/zos/skylark-tools/public/files/2022f03efbaba2245141b2f095caa839.png#align=left&display=inline&height=420&margin=%5Bobject%20Object%5D&originHeight=720&originWidth=1280&status=done&style=stroke&width=746)

# 接口调用

## 示例代码

### .json 示例代码

```json
{
  "defaultTitle": "Bluetooth"
}
```

### .acss 示例代码

```css
/* .acss */
.help-info {
  padding: 10px;
  color: #000000;
}
.help-title {
  padding: 10px;
  color: #fc0d1b;
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

Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| autoClose | Boolean | 否 | 表示是否在离开当前页面时自动断开蓝牙，不传值默认为 true。<br />**注意**：仅支持 Android 系统。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

### Function success

success 回调函数会携带一个 Object 类型的对象，其属性如下：

| **属性**     | **类型** | **描述**       |
| ------------ | -------- | -------------- |
| isSupportBLE | Boolean  | 是否支持 BLE。 |

## 错误码

| **错误码** | **说明**                   | **解决方案**               |
| ---------- | -------------------------- | -------------------------- |
| 1          | IDE 不支持调用该 API。   | 请在真机上调用。           |
| 12         | 蓝牙未打开。               | 请尝试打开蓝牙。           |
| 13         | 与系统服务的链接暂时丢失。 | 请尝试重新连接。           |
| 14         | 未授权支付宝使用蓝牙功能。 | 请授权支付宝使用蓝牙功能。 |
| 15         | 未知错误。                 | -                          |
| 2001       | 用户不允许授权。                 | 请授权当前小程序使用蓝牙功能。|
| 2002       | 用户不允许授权，且勾选了“总是保持以上选择，不再询问“后，再次调用该接口。                | 请授权当前小程序使用蓝牙功能。|
| 2003       | 用户不允许授权，且勾选了“总是保持以上选择，不再询问”。 | 请授权当前小程序使用蓝牙功能。|

