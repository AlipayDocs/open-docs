## 错误码
2001

## 报错描述
my.getLocation 获取用户地理位置时报 error: 2001（用户拒绝给小程序授权）。 

## 涉及接口
[my.getLocation](https://opendocs.alipay.com/mini/api/mkxuqd)

## 报错原因
my.getLocation 获取用户地理位置时用户拒绝给小程序授权地理位置获取权限导致。 

## 解决方案

- 建议在需要获取用户地理位置前，增加获取权限的用途和引导提示，引导用户接受小程序授权，增加用户体验。
- my.getLocation 重新发起 API 调用。
