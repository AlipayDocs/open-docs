## 错误码
14

## 报错描述
my.openBluetoothAdapter 初始化小程序蓝牙模块时报 error: 14（未授权支付宝使用蓝牙功能）。 

## 涉及接口
[my.openBluetoothAdapter](https://opendocs.alipay.com/mini/api/kunuy4)

## 报错原因
my.openBluetoothAdapter 初始化小程序蓝牙模块时手机设备未授权支付宝客户端使用手机蓝牙功能导致。 

## 解决方案

- 引导用户打开手机的系统设置界面，在应用权限中找到支付宝客户端并开启授权蓝牙功能的使用权限，可通过 [my.showAuthGuide](https://opendocs.alipay.com/mini/api/show-auth-guide) 权限引导 API 进行引导。
- 开启授权蓝牙功能后重新推送小程序，调用 my.openBluetoothAdapter 做初始化操作。

 
