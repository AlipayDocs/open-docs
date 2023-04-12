# 简介

**onTabItemTap** 是切换标签（tab）时触发，可用于目标页面监听 tabBar 的点击事件。

相关问题可查看 [tabBar 常见问题](https://opendocs.alipay.com/mini/api/do7urq)。

## 使用限制

- 基础库 [1.11.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.32 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码

```javascript
//.js
Page({
  onTabItemTap(item) {
    console.log(item.index);
    console.log(item.pagePath);
    console.log(item.text);
  },
});
```

## 返回结果
Object 类型，参数如下：

| **参数** | **类型** | **描述** |
| --- | --- | --- |
| index | Number | 被点击 tabItem 的序号，从0开始。 |
| pagePath | String | 被点击 tabItem 的页面路径。 |
| text | String | 被点击 tabItem 的页面名称。 |
# Bug & Tip
-Tip 首次打开目标页面时，onTabItemTap 会在目标页面 onShow 后触发。重新回到目标页面时，onTabItemTap 会在目标页面 onShow 前触发。
