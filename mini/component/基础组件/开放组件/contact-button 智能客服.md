# 简介

智能客服能力由蚂蚁集团零号云客服提供。唤起智能客服组件，开通智能客服：进入对应小程序详情页 > **小程序信息** > **在线客服** 即可打开云客服免费使用。详情可查看 [智能客服](https://opendocs.alipay.com/b/03al9b)。

## 使用限制

- 版本要求基础库 1.14.1 或更高版本；支付宝客户端 10.1.10 或更高版本，若版本较低，建议做 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- **Native 渲染引擎**：暂不支持。可以通过 `my.canIUse('contact-button')` 判断是否支持。
- 智能客服仅支持企业用户。

# 使用

## 示例代码

### 集成咨询窗（必选）

```html
<contact-button tnt-inst-id="企业编码" scene="聊天窗编码" />
```

在云客服中进入 **设置** > **服务窗配置**，点击操作栏中的 **部署** ，获取 `tntInstId`（企业编码）和 `scene`（聊天窗编码）。

**说明：** 每个聊天窗编码都是唯一的。

![](https://cdn.nlark.com/yuque/0/2022/png/179989/1666578416135-8dd04eb5-caec-4f99-b4b7-ea9fd0ee9777.png)

### 自定义咨询按钮（可选）

```html
<contact-button
  tnt-inst-id="企业编码"
  scene="聊天窗编码"
  size="咨询按钮大小"
  color="咨询按钮颜色"
  icon="咨询按钮图片url"
/>
```

默认咨询按钮如下：![](https://cdn.nlark.com/lark/0/2018/png/14456/1540978653403-b7e714e5-1850-4f70-a16d-02f519934a9c.png#align=left&display=inline&height=80&margin=%5Bobject%20Object%5D&originHeight=80&originWidth=93&status=done&style=none&width=51)<br />修改后咨询按钮如下：![](https://cdn.nlark.com/lark/0/2018/png/14456/1540978838133-fb2e4c3f-c787-498c-a22f-17b4ef3c2e36.png#align=left&display=inline&height=54&margin=%5Bobject%20Object%5D&originHeight=54&originWidth=54&status=done&style=none&width=54)

### 支付宝端内消息提醒（可选）

其中 alipay-card-no，ext-info 两个属性的说明详见下方的属性描述表格。

```html
<contact-button
  tnt-inst-id="企业编码"
  scene="聊天窗编码"
  alipay-card-no="2088用户ID"
  ext-info="扩展信息"
/>
```

提醒一：打开支付宝，中间位置显示提示，点击即进入对话窗。按一定的频率进行消息提醒，默认 30 分钟提醒一次。

![|168x247](https://cdn.nlark.com/lark/0/2018/png/14456/1540984972757-72ccf597-9c89-4c49-be2e-9082cf3d504d.png#align=left&display=inline&height=631&margin=%5Bobject%20Object%5D&originHeight=631&originWidth=429&status=done&style=none&width=168)

提醒二：服务提醒中显示客服回复的消息内容，点击即进入对话窗。

![|178x174](https://cdn.nlark.com/lark/0/2018/png/14456/1540985055959-eafc3a3e-a2b6-468e-9766-8f200e45abfe.png#align=left&display=inline&height=422&margin=%5Bobject%20Object%5D&originHeight=422&originWidth=432&status=done&style=none&width=178)

提醒三：**朋友** > **小程序** > **我的** 显示未读的客服消息，点击即进入对话窗。用户离开聊天窗期间客服发的消息会进行提醒。

![|233x414](https://mdn.alipayobjects.com/afts/img/A*DVsRQJVXhEoAAAAAAAAAAABkAa8wAA/1024w_1024h_1l.png?bz=openpt_doc&t=Sd-T3Y8FDP4FcXpjFrQ5PAAAAABkMK8AAAAA#align=left&display=inline&height=414&margin=%5Bobject%20Object%5D&originHeight=414&originWidth=233&status=done&style=none&width=233)

### 接入访客名片

通过 Java SDK 可以将零号云客服访客名片功能添加至支付宝小程序中，可查看 [支付宝小程序接入访客名片](https://tech.antfin.com/docs/2/96906)。

## 属性说明

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| tnt-inst-id | String | 必填。企业唯一编码，一个企业支付宝账号对应一个编码。 |
| scene | String | 必填。聊天窗编码，每个聊天窗的唯一编码。 |
| size | Number/String | 选填。咨询按钮大小，正方形设置边长（如 25\*25 px）。<br />**默认值：** 25<br />**版本要求：** 基础库 [1.9.0](https://opendocs.alipay.com/mini/framework/compatibility) 及以上、支付宝客户端 [1.12.0](https://opendocs.alipay.com/mini/framework/compatibility) 以及上支持 rpx 单位 |
| color | String | 选填。咨询按钮颜色，默认白底蓝色。<br />**默认值：** #00A3FF<br />**版本要求：** 基础库 [1.9.0](https://opendocs.alipay.com/mini/framework/compatibility) 及以上 |
| icon | ImgUrl | 选填。咨询按钮头像。<br />**版本要求：** 基础库 [1.9.0](https://opendocs.alipay.com/mini/framework/compatibility) 及以上 |
| alipay-card-no | String | 选填。支付宝访客用户 ID（2088 开头）。<br />**说明：** 客服回答问题时，如客户已离开咨询窗口，则通过推送消息到支付宝 card 中提醒客户。 |
| ext-info | String | 选填。该属性主要用于传递一些扩展信息给组件，以实现一些高级功能。该属性值的生成方式为：encodeURIComponent({"字段名":"字段值"})， 其中，字段名和字段值要根据实际使用的功能进行替换。<br />目前通过传入扩展信息可支持的 3 个功能：<br />1.访客名片。需传 cinfo 和 key 两个扩展字段，代码形如在云客服中进入 **设置** > **服务窗配置**，点击操作栏中的 **部署** ，获取 `tntInstId`（企业编码）和 `scene`（聊天窗编码）。`encodeURIComponent({"cinfo":"生成的 cinfo","key":"生成的key"})`，cinfo 和 key 的值说明 支付宝小程序接入访客名片；<br />2.聊天窗默认带出用户的小程序订单数据。需传 appId 字段，代码示例如：`encodeURIComponent({"appId":"商户小程序appid"})`<br />3.未读客服消息同步至"我的小程序-我的"。同样需传 appId 字段，代码示例如： `encodeURIComponent({"appId":"商户小程序appid"})`。 |

# 常见问题

## contact-button 组件写了没展示，如何查看聊天记录？

首先检查基础版本库是否匹配，然后在 **支付宝 APP** > **朋友** > **服务提醒** 中查看消息记录。

## 开通云客服没有加 contact-button 智能客服代码，为何有的手机上显示有的不显示客服图标？

进入 **小程序控制台** > **设置** > **小程序信息** > **在线客服**，选择是否显示客服图标。

## 如何获取 tntInstId（企业编码）和 scene（聊天窗编码）？

在 [云客服](https://csmng.cloud.alipay.com/ccm.htm#/home) 中进入 **设置** > **服务窗配置**，点击操作栏中的 **部署** ，获取 `tntInstId`（企业编码）和 `scene`（聊天窗编码）。
