## 错误码
2001

## 报错描述
my.scan 调用扫一扫扫码时报：{"error": 2001,"errorMessage":"用户不允许授权"}。

## ![](https://gw.alipayobjects.com/zos/sptworksff_prod/23ceb911-583b-464f-9291-d2f17251beaa.jpg#align=left&display=inline&height=354&margin=%5Bobject%20Object%5D&originHeight=1280&originWidth=720&status=done&style=none&width=199)

## 涉及接口
[my.scan](https://opendocs.alipay.com/mini/api/scan)

## 报错原因
my.scan 调用扫一扫扫码时用户拒绝给小程序授权相机权限导致。

## 解决方案

- 建议在调用扫一扫功能前，增加获取权限的用途和引导提示，引导用户接受小程序授权增加用户体验。
- 用户授权后 my.scan 重新发起 API 调用。
