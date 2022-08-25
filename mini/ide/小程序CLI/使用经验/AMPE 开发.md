# 简介

支付宝小程序遵从“轻量化部署”，“即用即走”原则；具备维护成本低，不占用智能设备空间和内存的优势，同时也具备了硬件拓展能力和调用系统应用的能力，使用小程序真正可以形成软件应用和智能硬件的完美融合。目前越来越多的智能设备开始使用支付宝小程序替代设备端原有的应用。

为方便智能设备开发者使用支付宝小程序，我们推出 miniu 小程序开发工具，miniu 具备小程序开发、小程序推送至智能设备预览、小程序上传审核的全链路能力；开发者还可以依据自己设备的屏幕尺寸，自定义小程序的尺寸大小。

## 一、开通 AMPE 开放计划

![|723x122](https://cdn.nlark.com/yuque/0/2021/png/179989/1618320657896-9f64161e-b274-41e4-bcdd-825c79f775b5.png#align=left&display=inline&height=145&margin=%5Bobject%20Object%5D&name=image.png&originHeight=290&originWidth=1728&size=107890&status=done&style=none&width=864)

AMPE 小程序在研发过程中不作为一个端单独透出，在加入《AMPE 开放计划》后，和支付宝端共用一套研发流程，共享版本信息。

加入《AMPE 开放计划》是小程序主体账号的主动行为，需要在开放平台中开通。

![|723x419](https://cdn.nlark.com/yuque/0/2021/png/179989/1618320695221-349f7606-ce63-4cd8-895c-15648f362be3.png#align=left&display=inline&height=803&margin=%5Bobject%20Object%5D&name=image.png&originHeight=1606&originWidth=2770&size=839323&status=done&style=none&width=1385)

在开通了《AMPE 开放计划》后，小程序上线后，会在 AMPE 平台的“小程序市场”中透出。厂家可在 AMPE 平台中绑定小程序，进而在设备中透出该小程序。

![|723x414](https://cdn.nlark.com/yuque/0/2021/png/179989/1618320708549-6027f5b1-f446-4207-b22e-2126b7bc79cb.png#align=left&display=inline&height=794&margin=%5Bobject%20Object%5D&name=image.png&originHeight=1588&originWidth=2778&size=1017128&status=done&style=none&width=1389)

## 二、入驻至上架全流程

开发支付宝小程序首先需要完成开放平台入驻，随后遵循创建 -> 上传开发版本 -> 设置体验版本 -> 提交审核 -> 灰度 -> 上架 -> 下架的研发流程。在开通《AMPE 开放计划》后，已上架过小程序包会自动同步至 AMPE。

![|723x272](https://cdn.nlark.com/yuque/0/2021/png/179989/1618320720144-11b9ad14-53c6-42ba-8e19-3a3e3cfc383b.png#align=left&display=inline&height=395&margin=%5Bobject%20Object%5D&name=image.png&originHeight=790&originWidth=2102&size=559252&status=done&style=none&width=1051)

## 三、开发工具及使用

> 使用 MiniU 中的 AMPE 场景进行真机预览和调试，需要先完成 AMPE 平台入驻。

智能设备大部分是横屏，或可横竖屏切换，因此需要研发工具支持横屏开发，MiniU 中默认支持 AMPE 研发场景，同时智能设备的真机预览、调试与手机 app 不同，智能设备无法扫码打开开发版本小程序，只能**sync 推送**至智能设备，完成**真机预览**和**调试**功能。

目前 MiniU 中对于 AMPE 的研发支持如下：

| 功能         | 支持情况 | 备注                           |
| ------------ | -------- | ------------------------------ |
| 本地构建     | 已支持   |                                |
| 云构建       | 已支持   | 当构建失败时，失败原因还未透出 |
| 智能设备宽屏 | 已支持   | 宽屏开发时，调试工具等需要优化 |
| 真机预览     | 已支持   |                                |
| 真机调试     | 已支持   |                                |
| sync 推送    | 已支持   |                                |

### 3.1、安装 miniu

```shell
npm i -g miniu  # 外部用户 - 全局安装
npm i -D miniu  # 外部用户 - 项目依赖

tnpm i -g miniu # 内部用户 - 全局安装
tnpm i -D miniu # 内部用户 - 项目依赖
```

若为全局安装，安装完成后执行 miniu -v 查看当前 MiniU 的版本。

### 3.2、 使用 miniu 开发小程序

#### 3.2.1 开启服务

##### - 全局安装

```shell
cd ${projectPath} && miniu dev # miniu 全局安装时
```

##### - 项目依赖

修改 package.json：

```json
{
	...
  "scripts": {
  	"dev": "miniu dev"
  },
  "devDependencies": {
  	"miniu": "1.12.1"
  },
  ...
}
```

然后执行 npm run dev。

上述两种命令执行后，会输出下图所示内容，在浏览器中打开 http://localhost:8000，开始使用 vscode + 浏览器的开发方式。

![|723x223](https://cdn.nlark.com/yuque/0/2021/png/179989/1618320744143-2f827b09-d891-412b-b7e3-212a5a2ee55d.png#align=left&display=inline&height=347&margin=%5Bobject%20Object%5D&name=image.png&originHeight=694&originWidth=2248&size=464148&status=done&style=none&width=1124)

#### 3.2.2 切换至 AMPE 场景

打开本地服务地址后，右侧面板切换至**Auth**面板，可以看到 AMPE 模块（若提示需要授权，那么先跳转至 3.2.5 节）。勾选“切换至 AMPE 开发场景”，即可切换至宽屏状态。

MiniU 中默认支持如下三种设备的开发，开发者也可自定义设备宽高以及 DRP：

- 1280X720
- 1920X720
- 960X1280

![|723x436](https://cdn.nlark.com/yuque/0/2021/png/179989/1618320754317-0c6a8a2f-e9c1-4092-92ae-a9f72fa7a665.png#align=left&display=inline&height=837&margin=%5Bobject%20Object%5D&name=image.png&originHeight=1674&originWidth=2778&size=481742&status=done&style=none&width=1389)

#### 3.2.3 真机预览、调试

> 在使用真机预览和调试功能前，请先到开放平台完成“开通 AMPE 开放计划”，具体做法在上面已做详细说明。

上图中可看到真机预览和真机调试的入口。与支付宝小程序不同的是，AMPE 不支持扫码，需要将构建好的小程序包直接推送至智能设备，所以在使用真机预览或调试的功能之前，需要添加设备 ID。此外，在 AMPE 整体涉及中需要移动应用和产品，才能完成最终推送。

MiniU 默认会保存已添加的设备，方便下次直接完成真机预览和调试。

![|723x437](https://cdn.nlark.com/yuque/0/2021/png/179989/1618320768232-2c4921dd-768d-4fdb-82c5-05ff1828b95b.png#align=left&display=inline&height=839&margin=%5Bobject%20Object%5D&name=image.png&originHeight=1678&originWidth=2778&size=420777&status=done&style=none&width=1389)

点击真机预览或者调试，等待返回推送完成的提示后，在设备拉取最新的包进行预览。

![|421x918](https://intranetproxy.alipay.com/skylark/lark/0/2021/png/342910/1609745002864-1c38c24e-f735-4416-988d-6e57876ad974.png#align=left&display=inline&height=918&margin=%5Bobject%20Object%5D&originHeight=1836&originWidth=842&status=done&style=none&width=421)

#### 3.2.4 上传开发版本

上面提到过 AMPE 和支付宝共享应用信息和应用版本，AMPE 小程序没有独立的开发版本，所以上传的开发版本是支付宝的开发版本，上传时，可直接在 Auth 面板中点击“上传”按钮完成上传。

![|723x437](https://cdn.nlark.com/yuque/0/2021/png/179989/1618320784165-906562f6-e56c-4234-874e-e2b45349a52f.png#align=left&display=inline&height=839&margin=%5Bobject%20Object%5D&name=image.png&originHeight=1678&originWidth=2778&size=470807&status=done&style=none&width=1389)

#### 3.2.5 MiniU 授权登录

在使用 Auth 面板中的所有功能前，需要先完成授权登录。MiniU 授权登录使用公私钥+toolId 的方式，实现一次授权，永久登录。

##### 生成公私钥

点击“新建”，1s 左右后，复制生成的公钥。

![|706x444](https://cdn.nlark.com/yuque/0/2021/png/179989/1618320798204-924894a9-f230-4e2c-bc8e-50a2445af512.png#align=left&display=inline&height=444&margin=%5Bobject%20Object%5D&name=image.png&originHeight=888&originWidth=1412&size=170490&status=done&style=none&width=706)

![|691x545](https://cdn.nlark.com/yuque/0/2021/png/179989/1618320808683-1ab683e5-53df-44e5-ae0e-f380c7cbc2f1.png#align=left&display=inline&height=545&margin=%5Bobject%20Object%5D&name=image.png&originHeight=1090&originWidth=1382&size=467963&status=done&style=none&width=691)

##### 获取 toolId

打开生成提示中的链接，获取 toolId。

##### 完成配置

回到本地服务，输入 toolId，点击“保存”，完成最终配置。

更多请参见：[AMPE 小程序开发流程](https://opendocs.alipay.com/mini/01l9vi)。
