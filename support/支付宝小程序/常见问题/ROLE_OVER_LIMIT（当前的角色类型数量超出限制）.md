## 错误码
ROLE_OVER_LIMIT（当前的角色类型数量超出限制）。

## 错误描述
调用 alipay.open.app.members.create（应用添加成员接口）时报 ROLE_OVER_LIMIT（当前的角色类型数量超出限制）。

## 涉及接口
[alipay.open.app.members.create](https://opendocs.alipay.com/mini/03l21t)（应用添加成员接口）

## 报错原因
开发者和体验者都是有数量限制的，超出限制会报此错误。开发者数量限制为 30，体验者数量限制为 50。

## 解决方案
使用 [alipay.open.app.members.delete](https://opendocs.alipay.com/mini/03l3ex)（应用删除成员接口）删除相关成员后再进行邀请。
