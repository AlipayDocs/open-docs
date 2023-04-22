## 错误码
DEVELOPER_ALREADY_EXSIT（用户已是开发者或被邀请中）。

## 错误描述
调用 alipay.open.app.members.create（应用添加成员接口）时报 DEVELOPER_ALREADY_EXSIT（用户已是开发者或被邀请中）。

## 涉及接口
[alipay.open.app.members.create](https://opendocs.alipay.com/mini/03l21t)（应用添加成员）

## 报错原因
已经邀请了该支付宝账号，或者该支付宝账号已经是开发者。

## 解决方案
通过 [alipay.open.app.members.query](https://opendocs.alipay.com/mini/03l3ew)（应用查询成员列表）查询该支付宝账号是否已经是开发者，如果还在邀请中，需要被邀请者进行同意才能邀请成功。具体如下图所示，可以在支付宝首页腰封位置看到邀请信息，并同意邀请即可。<br />![](https://gw.alipayobjects.com/zos/sptworksff_prod/7026dc08-e9f3-4e87-be74-4d7aa4ac4447.png#align=left&display=inline&height=397&margin=%5Bobject%20Object%5D&originHeight=565&originWidth=316&status=done&style=none&width=222)
