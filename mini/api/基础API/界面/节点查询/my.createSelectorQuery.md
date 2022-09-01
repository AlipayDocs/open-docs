# 简介

**my.createSelectorQuery** 是用于返回一个 SelectorQuery 对象实例的 API。

## 使用限制

- 基础库 [1.4.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.8 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- `my.createSelectorQuery()` 检测渲染层上的所有节点。要限定检测范围，推荐使用 `this.createSelectorQuery()`。详情可查看 [页面运行机制](https://opendocs.alipay.com/mini/framework/page-detail#Page.prototype.createSelectorQuery)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验

![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/2acd429bacf285e962c28166b6c60b82.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=none&width=127)

# 接口调用

## 示例

[小程序在线](https://opendocs.alipay.com/openbox/mini/opendocs/create-selector-query?view=preview&defaultPage=pages/index/index&defaultOpenedFiles=pages/index/index&theme=light)

### .js 示例代码

```javascript
// API-DEMO page/API/create-selector-query/create-selector-query.js
Page({
  createSelectorQuery() {
    my.createSelectorQuery()
      .select('#non-exists')
      .boundingClientRect()
      .select('#one')
      .boundingClientRect()
      .selectAll('.all')
      .boundingClientRect()
      .select('#scroll')
      .scrollOffset()
      .selectViewport()
      .boundingClientRect()
      .selectViewport()
      .scrollOffset()
      .exec(ret => {
        console.log(ret);
        my.alert({
          content: JSON.stringify(ret, null, 2),
        });
      });
  },
});
```

### ret 结构

```json
[
  null,
  {
    "x": 1,
    "y": 2,
    "width": 1367,
    "height": 18,
    "top": 2,
    "right": 1368,
    "bottom": 20,
    "left": 1
  },
  [
    {
      "x": 1,
      "y": -34,
      "width": 1367,
      "height": 18,
      "top": -34,
      "right": 1368,
      "bottom": -16,
      "left": 1
    },
    {
      "x": 1,
      "y": -16,
      "width": 1367,
      "height": 18,
      "top": -16,
      "right": 1368,
      "bottom": 2,
      "left": 1
    }
  ],
  {
    "scrollTop": 0,
    "scrollLeft": 0
  },
  {
    "width": 1384,
    "height": 360
  },
  {
    "scrollTop": 35,
    "scrollLeft": 0
  }
]
```

## 返回值

返回值为 [SelectorQuery](https://opendocs.alipay.com/mini/api/pc8s51)。
