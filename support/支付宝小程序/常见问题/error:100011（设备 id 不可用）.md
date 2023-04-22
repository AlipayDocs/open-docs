# 错误码
10011

## 报错描述
调用 my.writeBLECharacteristicValue、my.readBLECharacteristicValue、my.notifyBLECharacteristicValueChange 等蓝牙 API 时，报错 error:10011,errorMessage:"设备 id 不可用" 。

## 涉及接口
[my.writeBLECharacteristicValue](https://opendocs.alipay.com/mini/api/vmp2r4)、[my.readBLECharacteristicValue](https://opendocs.alipay.com/mini/api/zro0ka)、[my.notifyBLECharacteristicValueChange](https://opendocs.alipay.com/mini/api/pdzk44) 等 [蓝牙 API](https://opendocs.alipay.com/mini/api/bluetooth-intro)。

## 报错原因
调用 API 时入参 deviceId 不可用，或为空。

## 解决方案

- 检查 deviceId 入参值是否正确。
- 可使用 [my.getBLEDeviceServices](https://opendocs.alipay.com/mini/api/uzsg75) 获取设备 deviceId，可参考官网 [蓝牙 API 概览](https://opendocs.alipay.com/mini/api/bluetooth-intro) 进行调用集成。
