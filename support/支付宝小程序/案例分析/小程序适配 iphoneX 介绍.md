# 小程序适配 iphoneX 步骤
涉及适配的主要有自定义导航栏（NavigationBar）、自定义标签栏（TabBar）以及页面底部的吸底按钮（使用官方组件进行开发，不需要自行适配）。

1. 根据 iPhone 官方文档，iPhoneX 顶部状态栏的适配安全区域高度为 44pt，底部操作条区域高度为 34pt（一些系统 Bar 的默认高度设备可能会变化，建议以官网给出的为准）。<br />也可在 .acss 中使用 `safe-area-inset-bottom`、`safe-area-inset-top` 分别对iPhoneX 顶部状态栏的安全区域高度、底部操作条区域高度进行兼容，例如：
```css
/** button.acss **/
.sm-button {
  margin-top: env(safe-area-inset-top);
  margin-bottom: env(safe-area-inset-bottom);
}
```

2. 通过 [my.getSystemInfo](https://opendocs.alipay.com/mini/api/system-info) 获取设备信息，判断出 iPhoneX 设备类型；<br />**注意**：
   - model 值的格式： iPhone X(GSM+CDMA)<iphone10,3>，因此需要用字符串检索匹配进行判断。
   - 建议设置 globalData 全局数据增加一个适配标识，在 onLaunch 中调用适配逻辑。
3. 自定义标题栏详情可查看 [设置小程序标题栏透明介绍](https://opendocs.alipay.com/support/01rb0y)；自定义标签栏（TabBar）以及页面底部的吸底按钮，可以通过小程序的 [my.navigateTo](https://opendocs.alipay.com/mini/api/zwi8gx) 自行实现。

**注意**：样式像素换算可查看 [ACSS 语法参考](https://opendocs.alipay.com/mini/framework/acss)。

# 判断 iphoneX 系列的手机机型
通过 my.getSystemInfo 接口返回的 model 参数判断机型，iPhone X model 参数返回 iPhone10,3 或 iPhone10,6，以此为判断依据。<br />对于 iPhone，model 参数将返回 iPhone 内部代码（Internal Name）。<br />iPhone 手机型号与对应的 model 返回值可查看 [model 参数](https://opendocs.alipay.com/mini/api/system-info#Function%20success)（以苹果官方提供的为准）。
