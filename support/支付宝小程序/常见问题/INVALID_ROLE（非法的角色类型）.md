## 错误码
INVALID_ROLE（非法的角色类型）。 

## 错误描述
调用 alipay.open.app.members.create（应用添加成员接口）时报 INVALID_ROLE（非法的角色类型）。 

## 涉及接口

- [alipay.open.app.members.create](https://opendocs.alipay.com/mini/03l21t)（应用添加成员）
- [alipay.open.app.members.delete](https://opendocs.alipay.com/mini/03l3ex) (应用删除成员)
- [alipay.open.app.members.query](https://opendocs.alipay.com/mini/03l3ew) (应用查询成员列表)

## 报错原因
传入的 role 只支持 DEVELOPER 和 EXPERIENCER 两种类型。

- DEVELOPER-开发者
- EXPERIENCER-体验者

## 解决方案
传入正确的 role 类型，如 DEVELOPER、EXPERIENCER。<br /> <br /> 
