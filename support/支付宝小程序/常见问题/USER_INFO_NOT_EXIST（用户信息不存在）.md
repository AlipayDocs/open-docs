## 错误码
USER_INFO_NOT_EXIST（用户信息不存在）。 

## 错误描述
调用 alipay.open.app.members.create（应用添加成员接口）时报 USER_INFO_NOT_EXIST（用户信息不存在）。 

## 涉及接口
[alipay.open.app.members.create](https://opendocs.alipay.com/mini/03l21t)（应用添加成员）

## 报错原因
传入的 logon_id 非支付宝登录账号。 

## 解决方案
在支付宝客户端 > 我的 > 点击个人信息 > 支付宝账号查看并使用当前支付宝登录账号作为 logon_id 传入。<br /> 
