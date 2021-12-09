- 错误码信息及解决方案，请参见 [蓝牙 API 错误码对照表](https://opendocs.alipay.com/mini/api/ucd2lh)。<br />
- 常见问题及解决方法，请参见 [蓝牙 API FAQ](https://opendocs.alipay.com/mini/0090tx)。<br />

# 版本需求
| **蓝牙类型** | **支付宝客户端版本需求** | **Android 或 iOS 版本需求** |
| --- | --- | --- |
| BLE 低功耗蓝牙 | 支付宝客户端 10.0.18 或更高版本，若版本较低，建议做 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。 | <ul><li>Android： 5.0 及以上版本</li><li>iOS：无版本需求</li><ul/>
| 传统蓝牙 | <ul><li>支付宝客户端 10.0.18 或更高版本，若版本较低，建议做 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。</li><li>[my.startBluetoothDevicesDiscovery](https://opendocs.alipay.com/mini/api/ksew43) 方法的 allowDuplicatesKey 和 interval 参数，从支付宝客户端 10.0.20 版本开始支持。</li><ul/>| - |
| iBeacon | 支付宝客户端 10.1.8 或更高版本，若版本较低，建议做 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。 | - |


# 基本流程

## 低功耗蓝牙流程图
![|865x1230](http://mdn.alipayobjects.com/afts/img/A*2egbR7frSkQAAAAAAAAAAABkAa8wAA/original?bz=openpt_doc&t=TUxB_ER0pgWwRjuYfxHU1QAAAABkMK8AAAAA#align=left&display=inline&height=1230&margin=%5Bobject%20Object%5D&originHeight=1230&originWidth=865&status=done&style=stroke&width=865)

## 传统蓝牙流程图
![|723x756](http://mdn.alipayobjects.com/afts/img/A*FoPBTqHoP1sAAAAAAAAAAABkAa8wAA/original?bz=openpt_doc&t=ahoz2azNPv_9wUCIO3OU3wAAAABkMK8AAAAA#align=left&display=inline&height=887&margin=%5Bobject%20Object%5D&originHeight=887&originWidth=848&status=done&style=stroke&width=848)

# 蓝牙 API
| **蓝牙类型** | **名称** | **功能说明** |
| --- | --- | --- |
| 低功耗蓝牙 | [my.connectBLEDevice](https://opendocs.alipay.com/mini/api/tmew6e) | 连接低功耗蓝牙设备。 |
|  | [my.setBLEMTU](https://opendocs.alipay.com/mini/api/my.setblemtu) | 设置低功耗蓝牙设备最大传输单元（MTU）。需在 [my.connectBLEDevice](https://opendocs.alipay.com/mini/api/tmew6e) 调用成功后调用，mtu 设置范围（22, 512）。 |
|  | [my.getBLEMTU](https://opendocs.alipay.com/mini/api/my.getblemtu) | 获取低功耗蓝牙设备的最大传输单元（MTU）。 |
|  | [my.disconnectBLEDevice](https://opendocs.alipay.com/mini/api/yqrmmk) | 断开与低功耗蓝牙设备的连接。 |
|  | [my.getBLEDeviceCharacteristics](https://opendocs.alipay.com/mini/api/fmg9gg) | 获取蓝牙设备所有 characteristic（特征值）。 |
|  | [my.getBLEDeviceServices](https://opendocs.alipay.com/mini/api/uzsg75) | 获取所有已发现的蓝牙设备，包括已经和本机处于连接状态的设备。 |
|  | [my.getBLEDeviceRSSI](https://opendocs.alipay.com/mini/api/my.getbledevicerssi) | 获取蓝牙低功耗设备的信号强度（Received Signal Strength Indication, RSSI）。 |
|  | [my.notifyBLECharacteristicValueChange](https://opendocs.alipay.com/mini/api/pdzk44) | 启用低功耗蓝牙设备特征值变化时的 notify 功能。 |
|  | [my.offBLECharacteristicValueChange](https://opendocs.alipay.com/mini/api/dlxobk) | 取消监听低功耗蓝牙设备的特征值变化的事件。 |
|  | [my.offBLEConnectionStateChanged](https://opendocs.alipay.com/mini/api/xfuy7k) | 取消低功耗蓝牙连接状态变化事件的监听。 |
|  | [my.onBLECharacteristicValueChange](https://opendocs.alipay.com/mini/api/cdu501) | 监听低功耗蓝牙设备的特征值变化的事件。 |
|  | [my.onBLEConnectionStateChanged](https://opendocs.alipay.com/mini/api/utgyiu) | 监听低功耗蓝牙连接的错误事件，包括设备丢失，连接异常断开等。 |
|  | [my.readBLECharacteristicValue](https://opendocs.alipay.com/mini/api/zro0ka) | 读取低功耗蓝牙设备特征值中的数据。 |
|  | [my.writeBLECharacteristicValue](https://opendocs.alipay.com/mini/api/vmp2r4) | 向低功耗蓝牙设备特征值中写入数据。 |
|  | [my.showBLEPermissionGuide](https://opendocs.alipay.com/mini/02pexh) | 蓝牙统一授权/开关引导流程。 |
|  | [my.getBLEDeviceStatus](https://opendocs.alipay.com/mini/02pdp9) | 获取设备蓝牙授权和开关状态。 |
| 传统蓝牙 | [my.closeBluetoothAdapter](https://opendocs.alipay.com/mini/api/wvko0w) | 关闭本机蓝牙模块。 |
|  | [my.getBluetoothAdapterState](https://opendocs.alipay.com/mini/api/eid4o6) | 获取本机蓝牙模块状态。 |
|  | [my.getBluetoothDevices](https://opendocs.alipay.com/mini/api/pelizr) | 获取所有已发现的蓝牙设备，包括已经和本机处于连接状态的设备。 |
|  | [my.getConnectedBluetoothDevices](https://opendocs.alipay.com/mini/api/ge8nue) | 获取处于已连接状态的设备。 |
|  | [my.offBluetoothAdapterStateChange](https://opendocs.alipay.com/mini/api/ocgwfe) | 移除本机蓝牙状态变化的事件的监听。 |
|  | [my.offBluetoothDeviceFound](https://opendocs.alipay.com/mini/api/snw2t7) | 移除寻找到新的蓝牙设备事件的监听。 |
|  | [my.onBluetoothDeviceFound](https://opendocs.alipay.com/mini/api/mhzls9) | 搜索到新的蓝牙设备时触发此事件。 |
|  | [my.onBluetoothAdapterStateChange](https://opendocs.alipay.com/mini/api/eegfbk) | 监听本机蓝牙状态变化的事件。 |
|  | [my.openBluetoothAdapter](https://opendocs.alipay.com/mini/api/kunuy4) | 初始化小程序蓝牙适配器。 |
|  | [my.startBluetoothDevicesDiscovery](https://opendocs.alipay.com/mini/api/ksew43) | 开始搜寻附近的蓝牙外围设备。 |
|  | [my.stopBluetoothDevicesDiscovery](https://opendocs.alipay.com/mini/api/syb4mi) | 停止搜寻附近的蓝牙外围设备。 |
|  | [my.makeBluetoothPair](https://opendocs.alipay.com/mini/api/makebluetoothpair) | 蓝牙配对接口。连接蓝牙之前，部分设备需要先配对。 |
|  | [my.cancelBluetoothPair](https://opendocs.alipay.com/mini/01zarv) | 取消蓝牙设备配对。 |
|  | [my.getBluetoothPairs](https://opendocs.alipay.com/mini/01zdnf) | 获取已经配对的蓝牙设备。  |
| iBeacon | [my.getBeacons](https://opendocs.alipay.com/mini/api/yqleyc) | 获取已经搜索到的 iBeacon 设备。 |
|  | [my.offBeaconServiceChange](https://opendocs.alipay.com/mini/api/offbeaconservicechange) | 取消监听 iBeacon 服务的状态变化。 |
|  | [my.offBeaconUpdate](https://opendocs.alipay.com/mini/api/offbeaconupdate) | 取消监听 iBeacon 设备的更新事件。 |
|  | [my.onBeaconServiceChange](https://opendocs.alipay.com/mini/api/rq1dl7) | 监听 iBeacon 服务的状态变化。 |
|  | [my.onBeaconUpdate](https://opendocs.alipay.com/mini/api/kvdg9y) | 监听 iBeacon 设备的更新事件。 |
|  | [my.startBeaconDiscovery](https://opendocs.alipay.com/mini/api/cy1g7k) | 开始搜索附近的 iBeacon 设备。 |
|  | [my.stopBeaconDiscovery](https://opendocs.alipay.com/mini/api/yp5owa) | 停止搜索附近的 iBeacon 设备。 |


# 示例代码
```javascript
//初始化
my.openBluetoothAdapter({
  success: (res) => {
  	console.log(res);
  }
});
//注册发现事件
my.onBluetoothDeviceFound({
  success: (res) => {
	let device = res.devices[0];
	//连接发现的设备
	my.connectBLEDevice({
	  deviceId: deviceId,
	  success: (res) => {
		console.log(res)
	  },
	  fail:(res) => {
	  },
	  complete: (res)=>{
	  }
	});
	//停止搜索
	my.stopBluetoothDevicesDiscovery({
	  success: (res) => {
		console.log(res)
	  },
	  fail:(res) => {
	  },
	  complete: (res)=>{
	  }
	});
  }
});
//注册连接事件
my.onBLEConnectionStateChanged({
  success: (res) => {
  	console.log(res);
	if (res.connected) {
		//开始读写notify等操作
        my.notifyBLECharacteristicValueChange({
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
	}
  }
});
//注册接收read或notify的数据
my.onBLECharacteristicValueChange({
  success: (res) => {
  	console.log(res);
  }
});
//开始搜索
my.startBluetoothDevicesDiscovery({
  services: ['fff0'],
  success: (res) => {
  	console.log(res)
  },
  fail:(res) => {
  },
  complete: (res)=>{
  }
});
//断开连接
my.disconnectBLEDevice({
  deviceId: deviceId,
  success: (res) => {
  	console.log(res)
  },
  fail:(res) => {
  },
  complete: (res)=>{
  }
});
//注销事件
my.offBluetoothDeviceFound();
my.offBLEConnectionStateChanged();
my.offBLECharacteristicValueChange();
//退出蓝牙模块
my.closeBluetoothAdapter({
  success: (res) => {
  },
  fail:(res) => {
  },
  complete: (res)=>{
  }
});
```
