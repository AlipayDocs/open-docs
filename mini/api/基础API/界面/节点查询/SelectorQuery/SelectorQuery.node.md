# 简介

**SelectorQuery.node** 是获取 Node 节点实例。目前支持 [Native Canvas](https://opendocs.alipay.com/mini/component/canvas) 的获取。

## 使用限制

- 基础库 [2.7.0](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

### .axml 示例代码

```xml
//page.axml
<canvas onReady="onCanvasReady" type="webgl" id="canvas" />
```

### .js 示例代码

```javascript
//page.js
Page({
  onCanvasReady() {
    my.createSelectorQuery()
      .select('#canvas')
      .node(res => {
        //console.log(res.node);
        const canvasContext = res.node.getContext('webgl');
        //...
      })
      .exec();
  },
});
```

## 入参

### Function callback

在执行 [SelectorQuery.exec](https://opendocs.alipay.com/mini/api/baz2hg) 方法后，返回节点信息。

## 回调参数

| **属性** | **类型** | **描述**               |
| -------- | -------- | ---------------------- |
| node     | Object   | 节点对应的 Node 实例。 |
