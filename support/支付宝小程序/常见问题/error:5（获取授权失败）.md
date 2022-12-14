## 错误码
5

## 报错描述
调用 my.openBluetoothAdapter、my.getBeacons 等蓝牙 API，my.chooseAlipayContact、my.choosePhoneContact 通讯录联系人 API 时报 error:5,errorMessage:"获取授权失败"。

## 涉及接口

- [my.openBluetoothAdapter](https://opendocs.alipay.com/mini/api/kunuy4)、[my.getBeacons](https://opendocs.alipay.com/mini/api/yqleyc) 等 [蓝牙 API](https://opendocs.alipay.com/mini/api/bluetooth-intro)。
- [my.chooseAlipayContact](https://opendocs.alipay.com/mini/api/ui-contact)、[my.choosePhoneContact](https://opendocs.alipay.com/mini/api/blghgl) 通讯录联系人API。

## 报错原因
调用 my.openBluetoothAdapter、my.getBeacons 等 蓝牙 API，my.chooseAlipayContact、my.choosePhoneContact 通讯录联系人 API 时弹出使用蓝牙/通讯录授权申请，用户拒绝了授权。

## 解决方案

- 为了创造更良好的支付宝小程序用户体验在用户充分了解小程序的业务内容后再引导用户授权，建议将小程序授权环节放在业务流程中，在调用蓝牙/通讯录API前，增加获取权限的用途和引导提示，提升用户体验。
- 在授权失败时做引导处理，重新调用相关蓝牙/通讯录API。
