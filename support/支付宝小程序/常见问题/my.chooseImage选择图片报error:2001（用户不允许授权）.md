## 错误码
2001

## 报错描述
使用手机设备功能 API（my.chooseImage、my.openBluetoothAdapter、添加手机联系人等）fail 返回 error：2001，errorMessage："用户不允许授权"。 

## 涉及接口

- [my.chooseImage](https://opendocs.alipay.com/mini/api/media/image/my.chooseimage)
- [my.openBluetoothAdapter](https://opendocs.alipay.com/mini/api/kunuy4)
- [my.addPhoneContact](https://opendocs.alipay.com/mini/api/contact)
- [my.scan](https://opendocs.alipay.com/mini/api/scan)

## 报错原因
用户第一次使用手机设备功能相册/摄像头/蓝牙等使用会弹出权限申请授权弹窗，用户点击了 **拒绝 **按钮。<br />![](https://gw.alipayobjects.com/zos/sptworksff_prod/7250d397-0a35-44c7-8ac2-5fc428c1177a.jpg#align=left&display=inline&height=563&margin=%5Bobject%20Object%5D&originHeight=2340&originWidth=1080&status=done&style=none&width=260) 

## 解决方案

- 为了创造更良好的支付宝小程序用户体验，建议在调用相关设备功能 API 前，增加引导提示。
- 在 fail 做引导处理，重新调用相关 API 使用手机设备功能。

 <br /> 
