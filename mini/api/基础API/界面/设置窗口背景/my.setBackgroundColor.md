# 简介

**my.setBackgroundColor** 是动态设置窗口的背景色的 API。

窗口背景色会在页面下拉或上滑操作时出现的区域呈现。  
my.setSetBackgroundColor 会覆盖 app.json 中所设置 window 的 backgroundColor，以及页面的 .json 文件中配置的 backgroundColor。

## 使用限制

此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 效果示例

![|723x407](https://gw.alipayobjects.com/zos/skylark-tools/public/files/0dcb3f8acde186bb18ebd5013ad2c4a8.png#align=left&display=inline&height=720&margin=%5Bobject%20Object%5D&originHeight=720&originWidth=1280&status=done&style=none&width=1280)

# 接口调用

## 示例代码

### .js 示例代码

```javascript
// .js
my.setBackgroundColor({
  backgroundColor: '#ffffff',
  backgroundColorTop: '#00ff00', // 仅对在 iOS 生效
  backgroundColorBottom: '#ff00ff', // 仅对在 iOS 生效
});
```

## 入参

入参为 Object 类型，属性如下：

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| backgroundColor | String（十六进制颜色码） | 否 | 窗口的背景色。 |
| backgroundColorTop | String（十六进制颜色码） | 否 | 顶部窗口的背景色，仅 iOS 支持。 |
| backgroundColorBottom | String（十六进制颜色码） | 否 | 底部窗口的背景色，仅 iOS 支持。 |
| success | Function | 否 | 接口调用成功的回调函数。 |
| fail | Function | 否 | 接口调用失败的回调函数。 |
| complete | Function | 否 | 接口调用结束的回调函数（调用成功、失败都会执行）。 |
