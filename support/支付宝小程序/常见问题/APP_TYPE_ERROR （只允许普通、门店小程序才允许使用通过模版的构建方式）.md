## 错误码
APP_TYPE_ERROR （只允许普通、门店小程序才允许使用通过模版的构建方式）。 

## 问题描述
通过 alipay.open.mini.version.upload（小程序基于模板上传版本）基于三方模板构建商家小程序版本报错：sub_code:"APP_TYPE_ERROR",sub_msg:"只允许普通、门店小程序才允许使用通过模版的构建方式"。 

## 涉及接口

- [alipay.open.mini.version.upload](https://opendocs.alipay.com/mini/03l8bz)（小程序基于模板上传版本）
- [alipay.open.app.mini.templatemessage.send](https://opendocs.alipay.com/mini/02cth2)（小程序发送模板消息）

## 解决方案
请检查公共参数入参：

- **app_id：**应传入第三方应用 APPID。
- **app_auth_token：**应传入**商家小程序授权第三方应用的授权码**，而非模板授权第三方用的授权码。

### 获取 app_auth_token
登录 [支付宝开放平台](https://open.alipay.com/platform/developerIndex.htm) > 进入第三方应用详情页 > **商家授权** > 找到已授权的小程序应用并获取 **授权token**（状态必须是 **生效中**）。<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/179989/1671071249867-39891c93-b6ae-4522-8aad-14c0f42254f3.png#align=left&display=inline&height=333&margin=%5Bobject%20Object%5D&name=image.png&originHeight=666&originWidth=1920&size=84421&status=done&style=none&width=960)
