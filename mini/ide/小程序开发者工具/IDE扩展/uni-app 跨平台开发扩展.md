# 简介

uni-app 跨平台开发扩展支持在支付宝小程序开发者工具（IDE）中将 uni-app 工程编译为微信、百度、字节跳动小程序。 请确保安装的是最新版本 IDE。

# 第一步 安装 uni-app 跨平台开发扩展

完成以下操作，安装 uni-app 开发扩展：

1. 打开 IDE，选择 **扩展市场** > **uni-app**，点击 **安装**。 ![|697x435](https://gw.alipayobjects.com/zos/skylark-tools/public/files/2c7bad3b2e98e7d0e46a1e35f11cdfea.jpeg?x-oss-process=image/resize,w_1500#align=left&display=inline&height=450&margin=%5Bobject%20Object%5D&originHeight=937&originWidth=1500&status=done&style=none&width=720)
1. 安装完成后，点击 **启用**。 ![|697x215](https://gw.alipayobjects.com/zos/skylark-tools/public/files/ac244999cdc8bb7c7c7a92b1b8f47ce2.jpeg#align=left&display=inline&height=222&margin=%5Bobject%20Object%5D&originHeight=380&originWidth=1230&status=done&style=none&width=720)

# 第二步 开启微信小程序编译

启用后，完成以下步骤开启微信小程序编译：

1. 在 IDE 上部菜单栏，选择 **扩展**>**uni-app 跨平台开发扩展**>**微信 IDE 调试**。<br/> **说明：** 请确保打开的是小程序 uni-app 项目工程，否则无法打开 uni-app 扩展配置页面。 ![|697x130](https://cdn.nlark.com/yuque/0/2021/png/179989/1625552782936-3cd6ee5f-1a30-44a3-adb6-19a1a58ea623.png#align=left&display=inline&height=306&margin=%5Bobject%20Object%5D&name=1581329759305-14dc7c2f-81b9-4b4a-930f-36c0f03fd26f.png&originHeight=306&originWidth=1638&size=260892&status=done&style=none&width=1638)
1. 在微信开发者工具路径文本框中输入微信开发者工具的安装路径，单击 **保存**。 微信开发者工具的默认安装路径如下，请根据实际情况输入。
   - MacOS：/Applications/wechatwebdevtools.app
   - Windows：C:/Program Files (x86)/Tencent/微信 web 开发者工具。**说明：**
     - 只有首次使用时需要配置 IDE 安装路径
     - 微信开发者工具必须打开服务端口，否则无法唤醒 IDE。详细信息可查看 微信开发文档 - 工具 - 安全设置。![|641x187](https://cdn.nlark.com/yuque/0/2021/png/179989/1625552800860-2f96437a-1734-4970-9192-b1c647217ac2.png#align=left&display=inline&height=556&margin=%5Bobject%20Object%5D&name=1581329863986-f629796e-b5fd-4baa-b1cc-b402f51ecf7f.png&originHeight=556&originWidth=1908&size=220332&status=done&style=none&width=1908)
1. 点击 **开始编译**。编译后，若 IDE 路径配置正确，并自动打开微信小程序 IDE，并加载编译后的微信小程序产物。

# 第三步 开启字节跳动编译

1. 在 IDE 上部菜单栏，选择 **扩展**>**uni-app 跨平台开发扩展**>**字节跳动 IDE 调试。**
1. 点击 **安装依赖** 进行安装
1. 根据需要点击 **开发编译** 或 **生产编译**。<br/> 开发编译和生产编译，产物路径是相同的。 ![|697x583](https://cdn.nlark.com/yuque/0/2021/png/179989/1625552825548-3cd3d397-820a-423f-a61e-a8907021f32f.png#align=left&display=inline&height=1422&margin=%5Bobject%20Object%5D&name=1581330081577-d8606edf-fb73-44ce-9b5f-7a257bffa5f9.png&originHeight=1422&originWidth=1702&size=333431&status=done&style=none&width=1702)

## 第四步 开启百度小程序编译

1. 在 IDE 上部菜单栏，选择 **扩展**>**uni-app 跨平台开发扩展**>**百度 IDE 调试**。
1. 点击 **安装依赖** 进行安装。
1. 根据需要点击 **开发编译** 或 **生产编译**。<br/> 开发编译和生产编译，产物路径是相同的。 ![|697x594](http://mdn.alipayobjects.com/afts/img/A*rM4GSr9-op4AAAAAAAAAAAAAAa8wAA/original?bz=openpt_doc&t=_voN5jdGwdYWiyHig7yk0QAAAABkMK8AAAAA#align=left&display=inline&height=1125&margin=%5Bobject%20Object%5D&originHeight=1125&originWidth=1320&status=done&style=none&width=1320)
