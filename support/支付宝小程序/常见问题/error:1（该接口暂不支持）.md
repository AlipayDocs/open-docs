## 错误码
1

## 报错描述
在 IDE 上调用蓝牙、my.getPhoneNumber 等一些 API 时调试器报错：{error: 1, errorMessage: "该接口暂不支持"}。<br />![](https://gw.alipayobjects.com/zos/sptworksff_prod/76f0c085-6a42-404e-9171-0764cb54b40d.png#align=left&display=inline&height=413&margin=%5Bobject%20Object%5D&originHeight=568&originWidth=1032&status=done&style=none&width=750)

## 涉及接口
[my.openBluetoothAdapter](https://opendocs.alipay.com/mini/api/kunuy4)、[my.getPhoneNumber](https://opendocs.alipay.com/mini/api/getphonenumber) 等。

## 报错原因
由于模拟器不支持模拟蓝牙、my.getPhoneNumber 等一些 API 功能导致。

## 解决方案
IDE 编辑完成相关 API 代码逻辑后，使用真机调试/预览进行调试 API 功能。
