
## 概述
我们提供了三种调试方式模拟器 + 调试工具、手机端调试面板、远程调试，供开发者进行调试操作，可根据需要自行选择调试方式。

## 模拟器 + 调试工具
模拟器中模拟了大部分的真机 API，并且配有调试工具，建议先在模拟器中完成基础功能、样式的调试，然后在真机上验证和调试，最终运行效果以真机为准。

**说明：** 本地地址调试需要在 IDE 上调试，请勾选 **忽略 http 验证**。

### 模拟器
[模拟器](https://opendocs.alipay.com/mini/ide/simulator) 提供了如下功能：

- 设备模拟（尺寸、精度等）
- 编译日志、编译错误提示、刷新
- 支付宝 JsAPI 模拟，以及位置、蓝牙、启动参数等模拟接口自定义配置
![|697x437](https://cdn.nlark.com/lark/0/2018/gif/149/1533554602563-bac3c785-934a-4119-abc8-a8126f7be2b5.gif#align=left&display=inline&height=1932&margin=%5Bobject%20Object%5D&originHeight=1932&originWidth=3080&status=done&style=none&width=3080)

### 调试工具
配合模拟器，我们提供了定制化的 chrome devtool，在其基础上提供比如 axml 等扩展。默认展示的有：

- **AXML：** 基于小程序元素的 dom、css 调试
- **Console：** 运行日志、错误查看
- **Storage：** 缓存数据查看、编辑
- **Sources：** 源码查看、断点调试
- **Network：** 网络资源、请求查看

![|723x456](https://cdn.nlark.com/lark/0/2018/png/149/1533554666150-b1e08ff6-2d1e-4eef-b068-14f7fc9180c6.png#align=left&display=inline&height=1956&margin=%5Bobject%20Object%5D&originHeight=1956&originWidth=3104&status=done&style=none&width=3104)

##  调试面板

1. 真机预览小程序时，可以通过右上角按钮打开 **调试面板**。
![|324x652](http://mdn.alipayobjects.com/afts/img/A*9BCuTK-xHh4AAAAAAAAAAAAAAa8wAA/original?bz=openpt_doc&t=UmBrXgUtgR7syYpFKqyR0gAAAABkMK8AAAAA#align=left&display=inline&height=652&margin=%5Bobject%20Object%5D&originHeight=652&originWidth=324&status=done&style=none&width=324)

1. 点击 **打开调试** 后，在页面上会出现悬浮蓝色按钮 **调试面板**。
![|270x543](http://mdn.alipayobjects.com/afts/img/A*azZLTauec8wAAAAAAAAAAABkAa8wAA/original?bz=openpt_doc&t=VTp7XohW1kIgnrxhXDcmBwAAAABkMK8AAAAA#align=left&display=inline&height=543&margin=%5Bobject%20Object%5D&originHeight=543&originWidth=270&status=done&style=none&width=270)

1. 点击 **调试面板** 按钮，就可以看到调试面板了。
![|324x652](http://mdn.alipayobjects.com/afts/img/A*1bPmSbqlEIkAAAAAAAAAAAAAAa8wAA/original?bz=openpt_doc&t=IB-6ztJx-yMcvlioC95wVgAAAABkMK8AAAAA#align=left&display=inline&height=652&margin=%5Bobject%20Object%5D&originHeight=652&originWidth=324&status=done&style=none&width=324)<br/>
目前 **调试面板** 主要提供以下功能：
   - Log 页签：显示打印日志（可按日志级别查看）。
   - Storage 查看小程序缓存。
   - Network 查看接口请求。
   - Data 页面 data 数据。

## 远程调试
在远程调试模式中，IDE 和手机端建立起一个连接，在 IDE 端可以进行断点、运行时信息检查、Network/Storage 信息查看和远程日志查看等。详情请参见 [真机调试](https://opendocs.alipay.com/mini/ide/remote-debug)。
