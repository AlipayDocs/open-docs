## 错误码
12 

## 报错描述
集成调用 [蓝牙 API](https://opendocs.alipay.com/mini/api/ucd2lh) 时报 error: 12（蓝牙未打开）。 

## 涉及接口
openBluetoothAdapter、stopBluetoothDevicesDiscovery、disconnectBLEDevice、writeBLECharacteristicValue、getBluetoothDevices、stopBluetoothDevicesDiscovery、disconnectBLEDevice、getBLEDeviceServices、writeBLECharacteristicValue、getConnectedBluetoothDevices   等 [蓝牙 API](https://opendocs.alipay.com/mini/api/bluetooth-intro)。 

## 报错原因
调用蓝牙 API 时用户手机设备的蓝牙功能处于关闭状态导致。 

## 解决方案
引导用户打开手机设备蓝牙后，重新调用蓝牙 API。<br /> <br /> 
