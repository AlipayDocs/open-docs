# 错误码
11002

## 报错描述
调用集成 iBeacon 设备API 时，报错 error:11002,errorMessage:"location service unavailable" 。

## 涉及接口
[iBeacon 设备API](https://opendocs.alipay.com/mini/api/yqleyc)

## 报错原因
调用 iBeacon 设备API 时手机、设备位置服务不可用或未开启。

## 解决方案
检查位置服务，可尝试重新打开位置服务后结束进程重新进入小程序。<br />**注意：**

- iBeacon 需要位置权限。iOS 11 及以后版本的手机，通过手机控制中心的快捷开关打开蓝牙，无法使用 iBeacon，需要在 **设置 **> **蓝牙 **中开启蓝牙，方可使用。
- 建议在 [my.onBeaconUpdate](https://opendocs.alipay.com/mini/api/kvdg9y) 回调中处理发现到的 iBeacon 设备信息。
