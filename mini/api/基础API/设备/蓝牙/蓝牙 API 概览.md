- 错误码信息及解决方案，可查看 [蓝牙 API 错误码对照表](https://opendocs.alipay.com/mini/api/ucd2lh)。
- 常见问题及解决方法，可查看 [蓝牙 API FAQ](https://opendocs.alipay.com/mini/0090tx)。

# 版本需求

| **蓝牙类型** | **支付宝客户端版本需求** | **Android 或 iOS 版本需求** |
| --- | --- | --- |
| BLE 低功耗蓝牙 | 支付宝客户端 10.0.18 或更高版本，若版本较低，建议做 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。 | <ul><li>Android： 5.0 及以上版本</li><li>iOS：无版本需求</li></ul> |
| 传统蓝牙 | <ul><li>支付宝客户端 10.0.18 或更高版本，若版本较低，建议做 <b>兼容处理</b>。</li><li>[my.startBluetoothDevicesDiscovery](https://opendocs.alipay.com/mini/api/ksew43) 方法的 allowDuplicatesKey 和 interval 参数，从支付宝客户端 10.0.20 版本开始支持。</li></ul> | - |
| iBeacon | 支付宝客户端 10.1.8 或更高版本，若版本较低，建议做 <b>兼容处理</b>。 | - |

# 基本流程

## 低功耗蓝牙流程图

![|865x1230](http://mdn.alipayobjects.com/afts/img/A*2egbR7frSkQAAAAAAAAAAABkAa8wAA/original?bz=openpt_doc&t=TUxB_ER0pgWwRjuYfxHU1QAAAABkMK8AAAAA#align=left&display=inline&height=1230&margin=%5Bobject%20Object%5D&originHeight=1230&originWidth=865&status=done&style=stroke&width=865)

## 传统蓝牙流程图

![|723x756](http://mdn.alipayobjects.com/afts/img/A*FoPBTqHoP1sAAAAAAAAAAABkAa8wAA/original?bz=openpt_doc&t=ahoz2azNPv_9wUCIO3OU3wAAAABkMK8AAAAA#align=left&display=inline&height=887&margin=%5Bobject%20Object%5D&originHeight=887&originWidth=848&status=done&style=stroke&width=848)

# 蓝牙 API

<table>
  <tr>
    <th><b>蓝牙类型</b></th>
    <th><b>名称</b></th>
    <th><b>功能说明</b></th>
  </tr>
  <tr>
    <td rowspan="15">低功耗蓝牙</td>
    <td><a href="https://opendocs.alipay.com/mini/api/tmew6e">my.connectBLEDevice</a></td>
    <td>连接低功耗蓝牙设备。</td>
  </tr>
  <tr>
    <td><a href="https://opendocs.alipay.com/mini/api/my.setblemtu">my.setBLEMTU</a></td>
    <td>设置低功耗蓝牙设备最大传输单元（MTU）。需在 <a href="https://opendocs.alipay.com/mini/api/tmew6e">my.connectBLEDevice</a> 调用成功后调用，mtu 设置范围（22, 512）。</td>
  </tr>
  <tr>
    <td><a href="https://opendocs.alipay.com/mini/api/my.getblemtu">my.getBLEMTU</a></td>
    <td>获取低功耗蓝牙设备的最大传输单元（MTU）。</td>
  </tr>
  <tr>
    <td><a href="https://opendocs.alipay.com/mini/api/yqrmmk">my.disconnectBLEDevice</a></td>
    <td>断开与低功耗蓝牙设备的连接。</td>
  </tr>
  <tr>
    <td><a href="https://opendocs.alipay.com/mini/api/fmg9gg">my.getBLEDeviceCharacteristics</a></td>
    <td>获取低功耗蓝牙设备某个服务中所有特征（characteristic）。</td>
  </tr>
  <tr>
    <td><a href="https://opendocs.alipay.com/mini/api/uzsg75">my.getBLEDeviceServices</a></td>
    <td>获取指定低功耗蓝牙设备所有服务列表。</td>
  </tr>
  <tr>
    <td><a href="https://opendocs.alipay.com/mini/api/my.getbledevicerssi">my.getBLEDeviceRSSI</a></td>
    <td>获取蓝牙低功耗设备的信号强度（Received Signal Strength Indication, RSSI）。</td>
  </tr>
  <tr>
    <td><a href="https://opendocs.alipay.com/mini/api/pdzk44">my.notifyBLECharacteristicValueChange</a></td>
    <td>启用低功耗蓝牙设备特征值变化时的 notify 功能。</td>
  </tr>
  <tr>
    <td><a href="https://opendocs.alipay.com/mini/api/dlxobk">my.offBLECharacteristicValueChange</a></td>
    <td>取消监听低功耗蓝牙设备的特征值变化的事件。</td>
  </tr>
  <tr>
    <td><a href="https://opendocs.alipay.com/mini/api/xfuy7k">my.offBLEConnectionStateChanged</a></td>
    <td>取消低功耗蓝牙连接状态变化事件的监听。</td>
  </tr>
  <tr>
    <td><a href="https://opendocs.alipay.com/mini/api/cdu501">my.onBLECharacteristicValueChange</a></td>
    <td>监听低功耗蓝牙设备的特征值变化的事件。</td>
  </tr>
  <tr>
    <td><a href="https://opendocs.alipay.com/mini/api/utgyiu">my.onBLEConnectionStateChanged</a></td>
    <td>监听低功耗蓝牙连接的错误事件，包括设备丢失，连接异常断开等。</td>
  </tr>
  <tr>
    <td><a href="https://opendocs.alipay.com/mini/api/zro0ka">my.readBLECharacteristicValue</a></td>
    <td>读取低功耗蓝牙设备特征值中的数据。</td>
  </tr>
  <tr>
    <td><a href="https://opendocs.alipay.com/mini/api/vmp2r4">my.writeBLECharacteristicValue</a></td>
    <td>向低功耗蓝牙设备特征值中写入数据。</td>
  </tr>
  <tr>
    <td><a href="https://opendocs.alipay.com/mini/02pdp9">my.getBLEDeviceStatus</a></td>
    <td>获取设备蓝牙授权和开关状态。</td>
  </tr>
  <tr>
    <td rowspan="14">传统蓝牙</td>
    <td><a href="https://opendocs.alipay.com/mini/api/wvko0w">my.closeBluetoothAdapter</a></td>
    <td>关闭本机蓝牙模块。</td>
  </tr>
  <tr>
    <td><a href="https://opendocs.alipay.com/mini/api/eid4o6">my.getBluetoothAdapterState</a></td>
    <td>获取本机蓝牙模块状态。</td>
  </tr>
  <tr>
    <td><a href="https://opendocs.alipay.com/mini/api/pelizr">my.getBluetoothDevices</a></td>
    <td>获取所有已发现的蓝牙设备，包括已经和本机处于连接状态的设备</td>
  </tr>
  <tr>
    <td><a href="https://opendocs.alipay.com/mini/api/ge8nue">my.getConnectedBluetoothDevices</a></td>
    <td>获取处于已连接状态的设备。</td>
  </tr>
  <tr>
    <td><a href="https://opendocs.alipay.com/mini/api/ocgwfe">my.offBluetoothAdapterStateChange</a></td>
    <td>移除本机蓝牙状态变化的事件的监听。</td>
  </tr>
  <tr>
    <td><a href="https://opendocs.alipay.com/mini/api/snw2t7">my.offBluetoothDeviceFound</a></td>
    <td>移除寻找到新的蓝牙设备事件的监听。</td>
  </tr>
  <tr>
    <td><a href="https://opendocs.alipay.com/mini/api/mhzls9">my.onBluetoothDeviceFound</a></td>
    <td>搜索到新的蓝牙设备时触发此事件。</td>
  </tr>
  <tr>
    <td><a href="https://opendocs.alipay.com/mini/api/eegfbk">my.onBluetoothAdapterStateChange</a></td>
    <td>监听本机蓝牙状态变化的事件。</td>
  </tr>
  <tr>
    <td><a href="https://opendocs.alipay.com/mini/api/kunuy4">my.openBluetoothAdapter</a></td>
    <td>初始化小程序蓝牙适配器。</td>
  </tr>
  <tr>
    <td><a href="https://opendocs.alipay.com/mini/api/ksew43">my.startBluetoothDevicesDiscovery</a></td>
    <td>开始搜寻附近的蓝牙外围设备。</td>
  </tr>
  <tr>
    <td><a href="https://opendocs.alipay.com/mini/api/syb4mi">my.stopBluetoothDevicesDiscovery</a></td>
    <td>停止搜寻附近的蓝牙外围设备。</td>
  </tr>
  <tr>
    <td><a href="https://opendocs.alipay.com/mini/api/makebluetoothpair">my.makeBluetoothPair</a></td>
    <td>蓝牙配对接口。连接蓝牙之前，部分设备需要先配对。</td>
  </tr>
  <tr>
    <td><a href="https://opendocs.alipay.com/mini/01zarv">my.cancelBluetoothPair</a></td>
    <td>取消蓝牙设备配对。</td>
  </tr>
  <tr>
    <td><a href="https://opendocs.alipay.com/mini/01zdnf">my.getBluetoothPairs</a></td>
    <td>获取已经配对的蓝牙设备。</td>
  </tr>
  <tr>
    <td rowspan="7">iBeacon</td>
    <td><a href="https://opendocs.alipay.com/mini/api/yqleyc">my.getBeacons</a></td>
    <td>获取已经搜索到的 iBeacon 设备。</td>
  </tr>
  <tr>
    <td><a href="https://opendocs.alipay.com/mini/api/offbeaconservicechange">my.offBeaconServiceChange</a></td>
    <td>取消监听 iBeacon 服务的状态变化。</td>
  </tr>
  <tr>
    <td><a href="https://opendocs.alipay.com/mini/api/offbeaconupdate">my.offBeaconUpdate</a></td>
    <td>取消监听 iBeacon 设备的更新事件。</td>
  </tr>
  <tr>
    <td><a href="https://opendocs.alipay.com/mini/api/rq1dl7">my.onBeaconServiceChange</a></td>
    <td>监听 iBeacon 服务的状态变化。</td>
  </tr>
  <tr>
    <td><a href="https://opendocs.alipay.com/mini/api/kvdg9y">my.onBeaconUpdate</a></td>
    <td>监听 iBeacon 设备的更新事件。</td>
  </tr>
  <tr>
    <td><a href="https://opendocs.alipay.com/mini/api/cy1g7k">my.startBeaconDiscovery</a></td>
    <td>开始搜索附近的 iBeacon 设备。</td>
  </tr>
  <tr>
    <td><a href="https://opendocs.alipay.com/mini/api/yp5owa">my.stopBeaconDiscovery</a></td>
    <td>停止搜索附近的 iBeacon 设备。</td>
  </tr>
</table>

# 示例代码

```javascript
//初始化
my.openBluetoothAdapter({
  success: res => {
    console.log(res);
  },
});
//注册发现事件
my.onBluetoothDeviceFound(res => {
  let device = res.devices[0];
  //连接发现的设备
  my.connectBLEDevice({
    deviceId: device.deviceId,
    success: res => {
      console.log(res);
    },
    fail: res => {},
    complete: res => {},
  });
  //停止搜索
  my.stopBluetoothDevicesDiscovery({
    success: res => {
      console.log(res);
    },
    fail: res => {},
    complete: res => {},
  });
});
//注册连接事件
my.onBLEConnectionStateChanged(res => {
  console.log(res);
  if (res.connected) {
    //开始读写notify等操作
    my.notifyBLECharacteristicValueChange({
      deviceId: deviceId,
      serviceId: serviceId,
      characteristicId: characteristicId,
      success: res => {
        console.log(res);
      },
      fail: res => {},
      complete: res => {},
    });
  }
});
//注册接收read或notify的数据
my.onBLECharacteristicValueChange(res => {
  console.log(res);
});
//开始搜索
my.startBluetoothDevicesDiscovery({
  services: ['fff0'],
  success: res => {
    console.log(res);
  },
  fail: res => {},
  complete: res => {},
});
//断开连接
my.disconnectBLEDevice({
  deviceId: deviceId,
  success: res => {
    console.log(res);
  },
  fail: res => {},
  complete: res => {},
});
//注销事件
my.offBluetoothDeviceFound();
my.offBLEConnectionStateChanged();
my.offBLECharacteristicValueChange();
//退出蓝牙模块
my.closeBluetoothAdapter({
  success: res => {},
  fail: res => {},
  complete: res => {},
});
```
