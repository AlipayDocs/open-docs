## 错误码
10005

## 报错描述
调用 my.notifyBLECharacteristicValueChange 接口启用低功耗蓝牙设备特征值变化时，报错 error:10005,errorMessage:"没有找到指定特征值"。

## 涉及接口
[my.notifyBLECharacteristicValueChange](https://opendocs.alipay.com/mini/api/pdzk44)

## 报错原因
characteristicId 填写错误、目标外设特定 service 下不具备该特征。

## 解决方案
检查 characteristicId 是否正确、检查目标外设特定 service 下是否具备该特征，可参考官网 [蓝牙API概览](https://opendocs.alipay.com/mini/api/bluetooth-intro) 流程进行调用集成。
