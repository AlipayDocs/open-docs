
### Auth中有什么
- 授权完成永久登录
- 小程序列表查看、切换
- 小程序版本上传
- 真机预览、真机调试
- AMPE场景切换


### 什么时候需要Auth

- 小程序中使用了小程序插件
- 小程序中使用了 `my.getAuthCode`
- 切换当前的小程序
- 上传代码至开放平台
- 进行小程序的真机预览和调试
- AMPE小程序开发者


### 授权登录
> 小程序 CLI 在1.14.0后对登录进行了全新升级，可通过简单的扫码即可完成持久化地授权登录。


#### 版本号大于等于1.14.0

1. 切换至Auth面板

![|723x443](https://cdn.nlark.com/yuque/0/2021/png/179989/1620630205839-dfb0a1da-00d2-44ed-a813-d56518055806.png#align=left&display=inline&height=1176&margin=%5Bobject%20Object%5D&name=image.png&originHeight=1176&originWidth=1922&size=540990&status=done&style=none&width=1922)

2. 支付宝扫码等待完成授权登录

![|723x344](https://cdn.nlark.com/yuque/0/2021/png/179989/1620630265451-84abb6e3-f43e-485a-99fc-59e40fb3a86a.png#align=left&display=inline&height=908&margin=%5Bobject%20Object%5D&name=image.png&originHeight=908&originWidth=1912&size=342300&status=done&style=none&width=1912)

#### 版本号低于1.14.0

1. 切换至 Auth 面板

![723x275](https://intranetproxy.alipay.com/skylark/lark/0/2020/png/88085/1609318371130-5a1b08dd-5d1a-445d-8d75-ecd8953d9870.png?x-oss-process=image%2Fresize%2Cw_1500#align=left&display=inline&height=301&margin=%5Bobject%20Object%5D&originHeight=571&originWidth=1500&status=done&style=none&width=792)

2. 点击“新建”，创建密钥

![|723x201](https://intranetproxy.alipay.com/skylark/lark/0/2020/png/88085/1609318614851-df4c4291-eaaa-4277-9d57-bc0bf2884b76.png#align=left&display=inline&height=220&margin=%5Bobject%20Object%5D&originHeight=408&originWidth=1467&status=done&style=none&width=792)

3. 复制密钥并点击上述提示的2中链接到开放平台生成 toolId

![|723x425](https://intranetproxy.alipay.com/skylark/lark/0/2020/png/88085/1609318790106-cd283b8f-7e15-424b-9d8c-03f8a19b675c.png?x-oss-process=image%2Fresize%2Cw_1500#align=left&display=inline&height=465&margin=%5Bobject%20Object%5D&originHeight=881&originWidth=1500&status=done&style=none&width=792)

4.保存 toolId 至 auth 面板，完成授权登录。

![|723x294](https://intranetproxy.alipay.com/skylark/lark/0/2020/png/88085/1609318832388-47a80bb9-a1f9-4a9f-98e1-d66e726196e2.png#align=left&display=inline&height=322&margin=%5Bobject%20Object%5D&originHeight=365&originWidth=897&status=done&style=none&width=792)


### 小程序切换
> 当插件加载失败或者左侧模拟器无法正常渲染，可在此处确认是否选中了正确的小程序应用。

完成授权登录后，刷新页面，会在Auth面板中展示“我的小程序”，可在此切换当前小程序应用。

![|723x424](https://intranetproxy.alipay.com/skylark/lark/0/2021/png/88085/1614002094176-a609e7ac-6db1-4025-a608-81d57ad9ef18.png#align=left&display=inline&height=485&margin=%5Bobject%20Object%5D&name=image.png&originHeight=970&originWidth=1654&size=313391&status=done&style=none&width=827)

### 上传版本

1. 点击“上传”按钮

![|723x386](https://intranetproxy.alipay.com/skylark/lark/0/2021/png/88085/1614002207999-7e0378dd-00e0-4bde-9883-e2d72e082760.png#align=left&display=inline&height=509&margin=%5Bobject%20Object%5D&name=image.png&originHeight=1018&originWidth=1908&size=254892&status=done&style=none&width=954)

2. 弹层中会展示下一版本号，可手动修改下一版本号。

![|723x318](https://intranetproxy.alipay.com/skylark/lark/0/2021/png/88085/1614002284996-1da277a5-8716-4a58-a8cc-bff82c3adc4e.png#align=left&display=inline&height=423&margin=%5Bobject%20Object%5D&name=image.png&originHeight=846&originWidth=1922&size=230184&status=done&style=none&width=961)

### 真机预览&调试

- [真机预览](https://miniu.alipay.com/doc/preview-real-machine)
- [真机调试](https://miniu.alipay.com/doc/debug-real-machine)



### AMPE场景
详细文档可参考：[https://opendocs.alipay.com/mini/01l9vi](https://opendocs.alipay.com/mini/01l9vi)。

1. 勾选“切换至AMPE开发场景”

![|723x439](https://intranetproxy.alipay.com/skylark/lark/0/2021/png/88085/1614002481493-22a5051d-5f5c-4bbc-80f0-b01192d6a46b.png#align=left&display=inline&height=560&margin=%5Bobject%20Object%5D&name=image.png&originHeight=1120&originWidth=1844&size=248461&status=done&style=none&width=922)

2. 真机预览、真机调试

与支付宝等手机APP的真机预览和调试不同，AMPE的真机预览和调试需要提供具体的设备和产品。所以，在预览和调试开始之前，需要填写一些设备和产品信息。

MiniU会将填写的移动应用ID、产品ID、设备ID存储下来，供下次直接使用。

![|723x400](https://intranetproxy.alipay.com/skylark/lark/0/2021/png/88085/1614002645197-70a281ae-0d8a-4c60-95ef-149f78afde7d.png#align=left&display=inline&height=514&margin=%5Bobject%20Object%5D&name=image.png&originHeight=1028&originWidth=1860&size=194845&status=done&style=none&width=930)

![|723x472](https://intranetproxy.alipay.com/skylark/lark/0/2021/png/88085/1614002704663-f427b2bf-0489-49c5-b92a-35149474c265.png#align=left&display=inline&height=595&margin=%5Bobject%20Object%5D&name=image.png&originHeight=1190&originWidth=1824&size=238108&status=done&style=none&width=912)
