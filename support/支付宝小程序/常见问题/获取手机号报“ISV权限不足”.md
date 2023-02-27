
## 错误描述
调用 my.getPhoneNumber，报错** ISV权限不足**。

## 问题原因
服务商权限不足可能是由于未绑定获取会员手机号或未申请用户信息造成的。 

## 解决方案

1. 进入 [开放平台控制台](https://open.alipay.com/develop/manage) > 对应小程序详情页 > **产品绑定** 绑定 **获取会员手机号**。<br />![](https://cdn.nlark.com/yuque/0/2022/png/179989/1661931956108-d30527bc-ad74-4fc9-80ac-1b67c0a7e811.png#align=left&display=inline&height=531&margin=%5Bobject%20Object%5D&originHeight=531&originWidth=1864&status=done&style=none&width=1864)

 

2. 点击 **用户信息申请** 进入申请页面，点击 **申请权限** 申请用户手机号。<br />![](https://cdn.nlark.com/yuque/0/2022/png/179989/1661932190662-fdbdbe98-1a22-4c10-9afe-57fe87ca7a61.png#align=left&display=inline&height=304&margin=%5Bobject%20Object%5D&originHeight=304&originWidth=1836&status=done&style=none&width=1836)
<br />3. 填写申请原因、使用场景等信息，提交申请，等待审核。<br />![](https://gw.alipayobjects.com/zos/sptworksff_prod/5e1a9de6-f8ab-472e-b9c7-a6103c4e2fef.jpg#align=left&display=inline&height=499&margin=%5Bobject%20Object%5D&originHeight=499&originWidth=752&status=done&style=none&width=752)

 

## 注意事项

- 请确认后端代码中传入的 APPID 与 PID 需要绑定产品且申请用户信息的小程序与账号信息。
- 使用主账户申请信息。
- 若是无法申请或者申请审核失败，请到 [商家服务中心](https://b.alipay.com/index2.htm) 在线咨询或拨打商家服务热线 4007585858 咨询，服务时间为：8:00-24:00。

 <br /> 
