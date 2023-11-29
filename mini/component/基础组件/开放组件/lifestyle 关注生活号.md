# 简介

lifestyle 组件，实现了在小程序里关注生活号的能力。

## 使用限制

- 版本要求基础库 1.13.0 或更高版本；支付宝客户端 10.1.5 或更高版本，若版本较低，建议做 [兼容处理](/mini/framework/compatibility)。
- **Native 渲染引擎**：暂不支持。可以通过 `my.canIUse('lifestyle')` 判断是否支持。
- 用户未关注，可点击 **关注** 按钮直接在小程序内完成关注。
- 用户已关注，可点击组件跳转到对应的生活号。
- 仅支持已和当前小程序关联的生活号。
- 组件 lifestyle 中生活号 ID 即生活号 APPID。
- 使用属性 onFollow 可以在用户关注后，来实现控制关注生活号组件不显示。
- 如需修改样式，使用 view 组件将 lifeStyle 组件包裹，给 view 设置样式，acss 样式设置 lifeStyle 组件绝对定位并透明，宽高百分百即可。
- 如需进行代码调试，请使用真机调试，扫码体验以及 IDE 不支持部分调试效果。

## 效果示例

![](https://gw.alipayobjects.com/zos/skylark-tools/public/files/6fe57c3ac1bbb263ac7ff6d931e19123.png#align=left&display=inline&height=105&margin=%5Bobject%20Object%5D&originHeight=105&originWidth=371&status=done&style=none&width=371)

# 使用

## 示例代码

### .axml 示例代码

```plain
<!-- API-DEMO page/component/lifestyle/lifestyle.axml -->
<lifestyle public-id="your_lifestyle_id" />
```

## 属性说明

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| public-id | String | 必填，生活号 ID（即生活号 APPID），必须是当前小程序同账号主体且已关联的生活号。<br />**版本要求：** 基础库版本 [1.3.0](/mini/framework/compatibility) 及以上 |
| onFollow | EventHandle | 当用户关注生活号成功后执行。<br />**版本要求：** 基础库版本 [1.10.0](/mini/framework/compatibility) 及以上 |
| memo | String | 文案。支持商家自定义，最多展示一行。 |

# 相关文档

[关注/跳转生活号](https://opendocs.alipay.com/mini/introduce/bntnry)

# 常见问题
Q：如何通过API查询用户是否已经关注了生活号？
A：支付宝小程序有提供对应的接口[查询是否关注生活号](https://opendocs.alipay.com/apis/api_6/alipay.open.public.user.follow.query)
