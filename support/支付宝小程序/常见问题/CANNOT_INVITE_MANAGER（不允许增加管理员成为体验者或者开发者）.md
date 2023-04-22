## 错误码
CANNOT_INVITE_MANAGER（不允许增加管理员成为体验者或者开发者）。

## 错误描述
调用 alipay.open.app.members.create（应用添加成员）接口时报 CANNOT_INVITE_MANAGER（不允许增加管理员成为体验者或者开发者）。

## 涉及接口
[alipay.open.app.members.create](https://opendocs.alipay.com/mini/03l21t)（应用添加成员）

## 报错原因
传入的 logon_id 已经是该小程序的管理员。

## 解决方案
传入的 logon_id 已经是该小程序的管理员，并不再需要添加此账号为开发者/体验者。
