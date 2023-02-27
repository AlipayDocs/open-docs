# 简介
小程序官网对大部分的基础组件、扩展组件和 API 提供了[体验demo](https://opendocs.alipay.com/mini/introduce/demo)。<br />开发者可以通过demo体验自己关心的基础能力在真机上的实现效果，提前知晓是否符合需求场景。编写小程序项目代码时，也可以创建一个demo项目参考demo上对应能力的实现，借鉴或直接使用到自己的小程序项目内，提高基础能力开发效率。<br />![](https://gw.alipayobjects.com/zos/workflow/workflow/202002141581665434817_7269932fdd7f8ba760b50d8a119a60c0.png#align=left&display=inline&height=375&margin=%5Bobject%20Object%5D&originHeight=600&originWidth=1200&status=done&style=none&width=750)<br /> 

## 官方demo体验途径

1. 使用支付宝扫码，扫描下列二维码立即体验示例效果。<br />![](https://gw.alipayobjects.com/zos/skylark-tools/public/files/37daa426d7ff9385724ad798f0e0380b.png#align=left&display=inline&height=158&margin=%5Bobject%20Object%5D&originHeight=158&originWidth=127&status=done&style=none&width=127)

 

2. 使用支付宝首页搜索 **小程序官方示例**，进入小程序体验效果。
3. 在对应的 [基础组件](https://opendocs.alipay.com/mini/component)、[扩展组件](https://opendocs.alipay.com/mini/component-ext)、[API](https://opendocs.alipay.com/mini/api) 详情文档中，通过文档中提供的体验二维码扫码进行快速体验。

## 获取官方demo代码方式

1. 打开 IDE，选择小程序添加空白模板。![image.png](https://cdn.nlark.com/yuque/0/2021/png/179989/1622803643019-036d143e-7913-418e-84b0-7b2e5226feca.png#align=left&display=inline&height=700&margin=%5Bobject%20Object%5D&name=image.png&originHeight=700&originWidth=1000&size=133247&status=done&style=none&width=1000)
2. 选择支付宝端，点击 **下一步**。<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/179989/1622803693178-45627eaa-b7af-4b28-ae6d-03cb0b874443.png#align=left&display=inline&height=700&margin=%5Bobject%20Object%5D&name=image.png&originHeight=700&originWidth=1000&size=69439&status=done&style=none&width=1000)
3. 选择入门模板 API-Demo。<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/179989/1622803738134-c8982588-c273-4bd0-8e67-ed7b6fd1a242.png#align=left&display=inline&height=700&margin=%5Bobject%20Object%5D&name=image.png&originHeight=700&originWidth=1000&size=77090&status=done&style=none&width=1000)


## 小程序快速示例
针对各种场景，小程序快速示例提供了示例代码，开发者可直接在小程序开发者工具（简称 IDE）快速从模板示例创建小程序和插件项目，并可在此基础上进行复用和修改，从而提高学习和应用效率。<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/179989/1622803834050-2d6095a6-199b-4ac7-b76b-7a1caa45ebe5.png#align=left&display=inline&height=700&margin=%5Bobject%20Object%5D&name=image.png&originHeight=700&originWidth=1000&size=171504&status=done&style=none&width=1000)

# 基础组件、扩展组件和API使用报错一般自助排查

## 基础组件使用报错一般自助排查

- 确认当前环境基础库是否符合组件版本要求。  
- 检查导入的数据类型是否符合组件要求。
- 如果是样式不生效或渲染异常，检查是否为原生组件， 检查组件是否支持自定义样式（支持自定义样式会在属性列表中列出 class 属性）。
- 使用 IDE 调试器提供的样式选取功能，排查添加样式属性是否生效。
- 确认代码是否保存，可以使用快捷键 Ctrl+Shift+S 保存全部，tab/Ctrl+S 保存当前 tab。
- 可查看官方demo内的相关基础组件实现代码，参考具体写法。
- 实际呈现效果请以真机为准。
- 个别机型异常、Android 和 iOS 一端正常一端异常等无法自行解决的问题，请收集相关信息，如 APPID、支付宝客户端版本、手机类型、简易可复现demo代码（必要时收集复现支付宝账号，复现时间），咨询[在线技术支持](https://opensupport.alipay.com/support/home.htm?ant_source=antsupport)。

## 扩展组件使用报错一般自助排查
扩展组件是使用小程序自定义组件能力实现的，基于[小程序自定义组件规范](https://opendocs.alipay.com/mini/framework/custom-component-overview)。

- 检查是否已经安装对应扩展组件库，[UI 组件](https://ant-design-mini.antgroup.com)：antd-mini。
- 有些自定义组件属性和对象依赖 component2 编译，检查 IDE 模拟器右上角 > 详情 > 项目配置 > 启动component2编译 是否勾选启动。
- 可查看官方demo内的相关扩展组件实现代码，参考具体写法。
- 使用 IDE 调试器提供的样式选取功能，排查添加样式属性是否生效。
- 确认代码是否保存，可以使用快捷键 Ctrl+Shift+S 保存全部 tab/Ctrl+S 保存当前 tab。
- 实际呈现效果请以真机为准。
- 个别机型异常、Android 和 iOS 一端正常一端异常等无法自行解决的问题，收集相关信息，如 APPID、支付宝客户端版本、手机类型、简易可复现demo代码（必要时收集复现支付宝账号，复现时间），咨询[在线技术支持](https://opensupport.alipay.com/support/home.htm?ant_source=antsupport)。非小程序官方提供的组件请咨询组件提供者。

## API 使用报错一般自助排查

- 确认当前环境基础库是否符合 API 版本要求。  
- 可查看官方demo内的相关 API 实现代码，参考具体写法。
- 确认代码是否保存，可以使用快捷键 Ctrl+Shift+S 保存全部 tab/Ctrl+S 保存当前 tab。
- 查看调试器 console 是否有报错，根据报错提示检查对应代码段。
- 添加 fail 回调函数，打印 fail 函数的返回，根据具体错误修改。
- 部分 API 模拟器不一定支持 IDE 模拟，可在真机模式看下是否正常，实际效果请以真机为准。
- 个别机型异常、Android 和 iOS 一端正常一端异常等无法自行解决的问题，请收集相关信息，如 APPID、支付宝客户端版本、手机类型、简易可复现demo代码（必要时收集复现支付宝账号，复现时间），咨询[在线技术支持](https://opensupport.alipay.com/support/home.htm?ant_source=antsupport)。 

# 视频教程
官网提供了[视频教程](https://forum.alipay.com/college)，介绍常用小程序组件和API的使用。


