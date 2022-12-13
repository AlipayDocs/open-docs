## 错误码
13

## 报错描述
my.openBluetoothAdapter 初始化小程序蓝牙模块时报 error: 13（与系统服务的链接暂时丢失）。 

## 涉及接口
[my.openBluetoothAdapter](https://opendocs.alipay.com/mini/api/kunuy4)

## 报错原因
my.openBluetoothAdapter 初始化小程序蓝牙模块时设备的蓝牙功能在信号弱的时候可能会出现连接不上的情况。 

## 解决方案

- 请确认传入的 deviceId 是否正确，以及设备发出的信号是否足够强，在信号弱的时候可能会出现连接不上的情况。
- 查看传入 deviceId 是否已连接上。onBLEConnectionStateChanged 这个事件中可以监听连接状态变化，可使用 getConnectedBluetoothDevices 获取处于已连接状态的设备。
- 确认设备蓝牙正常，重新建立系统服务链接。

 <br /> 
