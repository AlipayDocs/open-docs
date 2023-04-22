## 错误码
DEV_MANAGER_ALREADY_EXIST（用户已经是开发者管理员，不能添加为应用成员）。

## 错误描述
调用 alipay.open.app.members.create（应用添加成员接口）时报 DEV_MANAGER_ALREADY_EXIST（用户已经是开发者管理员，不能添加为应用成员）。

## 涉及接口
[alipay.open.app.members.create](https://opendocs.alipay.com/mini/03l21t)（应用添加成员）

## 报错原因
传入的 logon_id 已经是开发者管理员，不能再进行邀请。

## 解决方案
传入的 logon_id 已经是开发者管理员，无需再进行邀请。开发者管理员本身具有开发和体验权限的。
