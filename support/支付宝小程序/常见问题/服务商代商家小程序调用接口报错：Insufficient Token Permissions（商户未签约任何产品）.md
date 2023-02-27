## 问题描述
服务商代商家小程序调用接口报错：Insufficient Token Permissions（商户未签约任何产品） 

## 涉及接口

- [alipay.open.mini.version.detail.query](https://opendocs.alipay.com/mini/03l9bu)（小程序版本详情查询）
- [alipay.open.mini.version.upload](https://opendocs.alipay.com/mini/03l8bz)（小程序基于模板上传版本）等代调用接口。 

## 报错原因
令牌权限不足，小程序应用被处罚下线。 

## 解决方案

- 确认授权令牌是否失效，应用授权前三方应用是否已经绑定相对应产品，可尝试重新应用授权。
- 若小程序应用被处罚下线，小程序应用处于下线状态没有调用开放平台接口权限；请服务商引导商家登录商家自己的[开放平台控制台](https://open.alipay.com/isv/taskManager.htm)，在消息代办任务中找到对应处罚消息，点击 **详情 ** 进行申诉，申诉通过，且小程序应用恢复上线状态，才可调用接口。<br />
![image.png](https://cdn.nlark.com/yuque/0/2022/png/179989/1662534845858-3cb40865-ec13-495a-a44b-2135edae93a1.png#align=left&display=inline&height=170&margin=%5Bobject%20Object%5D&name=image.png&originHeight=339&originWidth=1800&size=40606&status=done&style=none&width=900)

**注意：**

- 若只是被处罚下架版本，对服务商代商家调用接口无影响。
- 违规查阅路径及处罚操作可查看[小程序违规处理规则](https://opendocs.alipay.com/rules/rules_mini/nowgsa)。

