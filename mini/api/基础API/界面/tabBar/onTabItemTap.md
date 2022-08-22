# 简介

**onTabItemTap** 是切换标签（tab）时触发，可用于目标页面监听 tabBar 的点击事件、[my.switchTab](https://opendocs.alipay.com/mini/api/ui-tabbar) 跳转事件。

相关问题可查看 [tabBar 常见问题](https://opendocs.alipay.com/mini/api/do7urq)。

## 使用限制

- 基础库 [1.11.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.32 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码

```javascript
//.js
Page({
  onTabItemTap(item) {
    console.log(item.index)
    console.log(item.pagePath)
    console.log(item.text)
  }
})
```

## 返回结果
Object 类型，参数如下：

| **参数** | **类型** | **描述** |
| --- | --- | --- |
| from | String | api：通过 tabBar 的点击触发；user：通过 my.switchTab 跳转触发 |
| index | Number | 页面在 app.json 中设置的 tabbar items 数组下标。 |
| pagePath | String | 页面路径。 |
| text | String | 页面名称。 |
