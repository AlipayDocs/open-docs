### Q：调用 my.writeBLECharacteristicValue 的返回值是空对象吗？

A：不是，调用此 API 返回的是写入成功的值。

### Q：调用 my.onBLECharacteristicValueChange 为何监听不到？一定要先写入才能监听到吗？

A：是的，调用此 API 需要先写入才能监听到。为防止多次注册事件监听导致一次事件多次回调，建议每次调用 on 方法监听事件之前，先调用 off 方法，关闭之前的事件监听。

### Q：调用 my.writeBLECharacteristicValue 为何报错 10014？

A：10014 错误是由于发送的数据为空或者格式错误导致，建议检查写入的数据或 HEX 转化是否有错误。

### Q：调用 my.writeBLECharacteristicValue 写入特征值，使用 16 进制的数组可以吗？

A：不可以，写入特征值需要使用 16 进制的字符串，并限制在 20 字节内。

### Q：安卓和 iOS 获取到的 deviceId 格式分别是什么样的？

A：

- Android 获取到的是蓝牙的 mac 地址。如：`11:22:33:44:55:66`
- iOS 获取到的是蓝牙的 UUID。如：`00000000-0000-0000-0000-000000000000`

### Q：调用 [my.startBluetoothDevicesDiscovery](https://opendocs.alipay.com/mini/api/ksew43) 接口为何搜索不到设备？

A：请确保设备已发出广播。若接口传入 services，请确保设备的广播内容中包含 service 的 UUID。

### Q：为什么 [my.getBluetoothDevices](https://opendocs.alipay.com/mini/api/pelizr?pathHash=8596a9de) API 获取到的已发现的蓝牙设备比实际手机设置蓝牙中搜索到的多？

A：蓝牙在系统中调用和在支付宝中调用本质上都是调用的系统 API，但是因为调用的时间点不一样，所以扫描的结果会存在差异。

### Q：调用蓝牙 API 时如果不开启 GPS 定位，部分机型会报错：定位服务未开启。连接不了蓝牙？

A：小程序蓝牙功能需要依赖 GPS 定位，因为大概 5 分之一的手机蓝牙需要依赖 GPS。 建议接入蓝牙时先引导用户打开 GPS 定位服务。

### Q：如何解决连接设备失败?

A：请确保传入的 deviceId 正确，并且设备发出的信号足够强。在信号弱的情况下，可能会出现连接设备失败。

### Q：如何解决写 / 读数据失败？

A：

- 请确保传入的 deviceId、serviceId、characteristicId 格式正确。
- deviceId 已连接上（可调用 [my.onBLEConnectionStateChanged](https://opendocs.alipay.com/mini/api/utgyiu) 监听连接状态的变化；调用 [my.getConnectedBluetoothDevices](https://opendocs.alipay.com/mini/api/ge8nue) 获取处于已连接状态的设备。）
- 在连接状态下写入方法。
- 检查 characteristicId 属于此 service。
- 此特征值支持写 / 读。

### Q：如何收到数据通知？

A：

- 请确保已调用 [my.notifyBLECharacteristicValueChange](https://opendocs.alipay.com/mini/api/pdzk44) 方法，并且传入的参数正确。
- 传入的 characteristicId 特征值支持 notify 或 indicate 操作。
- 确保硬件已发出通知。
- 注意基本流程顺序，在连接之后就调用 [my.notifyBLECharacteristicValueChange](https://opendocs.alipay.com/mini/api/pdzk44) 方法。

### Q：为何事件回调会多次被调用？

A：由于多次匿名函数注册监听了同一事件。所以建议在每次调用 on 方法监听事件之前，先调用 off 方法关闭之前的事件监听。
