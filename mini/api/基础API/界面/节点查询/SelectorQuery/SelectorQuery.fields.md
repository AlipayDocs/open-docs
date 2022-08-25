# 简介

**SelectorQuery.fields** 用于获取节点的相关信息。需要获取的字段在 fields 中指定。

## 使用限制

- 基础库 [2.7.3](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。
- computedStyle 的优先级高于 size，当同时在 computedStyle 里指定了 width/height 并且设置 size: true，则会优先返回 computedStyle 获取到的 width/height。

# 接口调用

## 示例代码

### .axml 示例代码

```html
<view id="view1" data-a="1" data-b="2">
  <map id="map" style="height: 100px;width: 100px;" />
  <canvas
    id="canvas"
    type="2d"
    onReady="onCanvasReady"
    style="height: 300px; width: 300px;"
  />
</view>
```

### .js 示例代码

```javascript
Page({
  onCanvasReady() {
    const selectorQuery = my.createSelectorQuery();
    selectorQuery
      .select('#view1')
      .fields(
        {
          id: true,
          dataset: true,
          rect: true,
          size: true,
        },
        function (res) {
          console.log(res, res.dataset);
        }
      )
      .select('#map')
      .fields(
        {
          context: true,
          rect: true,
          computedStyle: ['height', 'width'],
        },
        function (res) {
          console.log(res, res.context);
        }
      )
      .select('#canvas')
      .fields(
        {
          node: true,
        },
        function (res) {
          console.log(res, res.node);
        }
      )
      .exec();
  },
});
```

## 入参

### Object fileds

指定需要获取的节点信息。

| **属性** | **类型** | **默认值** | **必填** | **描述** |
| --- | --- | --- | --- | --- |
| id | Boolean | false | 否 | 节点 id，基础库 [2.7.4](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 开始支持，可通过 `my.canIUse('createSelectorQuery.return.fields.object.id')` 检测。 |
| dataset | Boolean | false | 否 | 是否返回节点 dataset。 |
| rect | Boolean | false | 否 | 是否返回节点布局位置（`left` `right` `top` `bottom`）。 |
| size | Boolean | false | 否 | 是否返回节点尺寸（`width` `height`）。 |
| scrollOffset | Boolean | false | 否 | 否是否返回节点的 `scrollLeft` `scrollTop`，节点必须是 `scroll-view` 或者 `viewport`。 |
| computedStyle | `Array<String>` | [] | 否 | 指定样式名列表，返回节点对应样式名的当前值。 |
| context | Boolean | false | 否 | 是否返回节点对应的 Context 对象。 |
| node | Boolean | false | 否 | 是否返回节点对应的 Node 实例。 |

### Function callback

回调函数。在执行 [SelectorQuery.exec](https://opendocs.alipay.com/mini/api/baz2hg) 方法后，返回节点信息。

#### callback 参数

##### Object res

节点的相关信息。

# Bug & Tip

基础库 2.7.24 修复了 iOS 15 系统获取 computedStyle 异常的问题，点此查看 [详情](https://forum.alipay.com/mini-app/post/88401025)。
