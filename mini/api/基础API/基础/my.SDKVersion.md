
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

## Q：怎么才能升级基础库版本到最新或到指定的版本？
A：IDE 中可通过模拟器上方的“展开面板”按钮 -> “设置”，选择对应的基础库版本进行调试；真机运行时，以实际客户端中基础库版本为准，客户端内建了基础库自动更新逻辑，无法在小程序中控制；旧版支付宝客户端可能无法自动更新到最新的小程序基础库，需要升级客户端；此外也可参考 [此文档](https://opendocs.alipay.com/mini/framework/lib#%E8%AE%BE%E7%BD%AE%E6%9C%80%E4%BD%8E%E5%9F%BA%E7%A1%80%E5%BA%93%E7%89%88%E6%9C%AC) ，在后台指定小程序运行时要求的最低基础库版本。

## Q：IDE 中选择基础库版本号 2.x 后不生效，my.SDKVersion 仍然返回 1.x？
A：使用 1.x 版本的小程序升级到使用 2.x 需要人工指定（IDE 上目前提示不够完善），请在 IDE 上项目详情中勾选 `启用小程序基础库 2.0 构建`。升级到 2.x 的相关信息请参考 [此文档](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2)。
