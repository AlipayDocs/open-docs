## 错误码
11

## 报错描述
my.chooseImage 选择图片 fail 返回 error：11，errorMessage："User cancel select video"。 

## 涉及接口
[my.chooseImage](https://opendocs.alipay.com/mini/api/media/image/my.chooseimage)

## 报错原因
my.chooseImage 唤起选择图片界面时，用户没有选择返回的图片就点击左上角返回小程序，取消操作。 

## 解决方案

- 为了创造更良好的支付宝小程序用户体验，建议在选择图片前，增加引导提示。
- 在 fail 做引导处理，重新调用 my.chooseImage 选择图片。

