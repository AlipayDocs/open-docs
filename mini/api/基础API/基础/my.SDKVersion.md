
# 简介
**my.SDKVersion** 是获取基础库版本号的 API。

## 使用限制
此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验
![](https://gw.alipayobjects.com/zos/skylark-tools/public/files/fcc0c9ce29b9e4aaaafbff09963ab8f6.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=none&width=127)

## 效果示例
![](https://gw.alipayobjects.com/zos/skylark-tools/public/files/001a7b0119688f18184236143cc2c1e3.gif#align=left&display=inline&height=525&margin=%5Bobject%20Object%5D&originHeight=525&originWidth=300&status=done&style=none&width=300)

# 接口调用

## 示例代码

```javascript
Page({
  getSDKVersion() {
    my.alert({
      content: my.SDKVersion,
    });
  }, 
});
```

## 返回值
为 `String` 类型，表示基础库版本号。
