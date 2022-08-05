
# 简介
**my.SDKVersion** 是获取基础库版本号的 API。  

基础库是小程序的运行时框架，不同版本支付宝客户端、不同的时间点，基础库版本可能不同。可通过 my.SDKVersion 获取当前运行环境（IDE 或真机）中的基础库版本号。

关于基础库的更多知识，可通过 [此文档](https://opendocs.alipay.com/mini/framework/lib) 了解。

## 使用限制
此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验
![](https://gw.alipayobjects.com/zos/skylark-tools/public/files/fcc0c9ce29b9e4aaaafbff09963ab8f6.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=none&width=127)

## 效果示例
![](https://gw.alipayobjects.com/zos/skylark-tools/public/files/001a7b0119688f18184236143cc2c1e3.gif#align=left&display=inline&height=525&margin=%5Bobject%20Object%5D&originHeight=525&originWidth=300&status=done&style=none&width=300)

# 接口调用

## 示例代码

### .js 示例代码
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
基础库版本号，`string` 类型，如 "2.7.20"。

# 常见问题
## Q：IDE 中选择基础库版本号后不生效，怎么办？
A：如果项目本身使用了 1.x 的基础库，需要 IDE 的项目详情中勾选 `启用小程序基础库 2.0 构建`。
