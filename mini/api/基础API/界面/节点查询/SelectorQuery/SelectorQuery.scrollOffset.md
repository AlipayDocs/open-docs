
# 简介
**SelectorQuery.scrollOffset** 用于将当前选择节点的滚动信息放入查询结果。

## 使用限制

- [2.7.4](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2)开始支持 callback 参数，可通过 `my.canIUse('createSelectorQuery.return.scrollOffset.callback')` 检测。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。
# 接口调用

### .js 示例代码
```javascript
Page({
  onReady() {
    const selectorQuery = my.createSelectorQuery();
    selectorQuery
    .selectViewport()
    .scrollOffset(function(res) {
    	console.log(res);
    })
    .exec();
  }
})
```

## 入参

### function callback
回调函数，在执行 `SelectorQuery.exec` 方法后，节点信息会在 callback 中返回。 

#### callback 参数
**object res**

| **属性** | **类型** | **说明** |
| --- | --- | --- |
| id | String | 节点 id。 |
| dataset | Object | 节点的 dataset。 |
| scrollLeft | Number | 节点的水平滚动位置。 |
| scrollTop | Number | 节点的竖直滚动位置。 |

