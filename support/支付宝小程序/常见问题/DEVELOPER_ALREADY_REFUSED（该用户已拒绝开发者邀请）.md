## 错误码
DEVELOPER_ALREADY_REFUSED（该用户已拒绝开发者邀请）。

## 错误描述
调用 alipay.open.app.members.create(应用添加成员) 接口时报 DEVELOPER_ALREADY_REFUSED（该用户已拒绝开发者邀请）。

## 涉及接口
[alipay.open.app.members.create](https://opendocs.alipay.com/mini/03l21t)（应用添加成员接口）

## 报错原因
邀请支付宝账号成为小程序开发者，用户拒绝邀请后再次调用该接口邀请会报此错误。

## 解决方案
调用 [alipay.open.app.members.delete](https://opendocs.alipay.com/mini/03l3ex)（应用删除成员）先删除拒绝邀请者账号后再调用 alipay.open.app.members.create（应用添加成员）邀请。
