# 简介

**my.createIntersectionObserver** 用于创建并返回一个 [IntersectionObserver](https://opendocs.alipay.com/mini/api/intersectionobserver-overview) 对象实例。需在 `page.onReady` 之后执行 `my.createIntersectionObserver()`。

## 使用限制

- 基础库 [1.11.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.32 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility) 。
- `my.createIntersectionObserver()` 检测渲染层上的所有节点。要限定检测范围，推荐使用 `this.createIntersectionObserver()`。详情可查看 [页面运行机制](https://opendocs.alipay.com/mini/framework/page-detail#Page.prototype.createIntersectionObserver)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

### .axml 示例代码

```html
<!-- .axml -->
<view class="logo" style="width: 200px;height: 200px;background-color:blue"
  >11</view
>
```

### .js 示例代码

```javascript
// .js
Page({
  onReady() {
    my.createIntersectionObserver()
      .relativeToViewport({ top: 100, bottom: 100 })
      .observe('.logo', res => {
        console.log(res, 'intersectionObserver');
        console.log(res.intersectionRatio); // 相交区域占目标节点的布局区域的比例
        console.log(res.intersectionRect); // 相交区域
        console.log(res.relativeRect); // 参照区域的边界
        console.log(res.boundingClientRect); // 目标边界
        console.log(res.time); // 时间戳
        console.log(res.id);
      });
  },
});
```

## 入参

入参为 Object 类型，参数如下：

| **参数** | **类型** | **默认值** | **描述** |
| --- | --- | --- | --- |
| thresholds | Array\<Number\> | [0] | 一个数值数组，包含所有阈值。 |
| initialRatio | Number | 0 | 初始的相交比例，如果调用时检测到的相交比例与这个值不相等且达到阈值，则会触发一次监听器的回调函数。 |
| selectAll | Boolean | false | 是否同时观测多个目标节点（而非一个），如果设为 true ，observe 的 targetSelector 将选中多个节点（**注意**：同时选中过多节点将影响渲染性能）。  |
| dataset | Boolean | false | 目标节点的 dataset 信息。当 dataset 为 true 时，[IntersectionObserver.observe](https://opendocs.alipay.com/mini/api/pra7yc) 回调中的 res 对象，会携带目标节点的 dataset 属性。。<br />基础库 [2.7.0](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 起支持。 |

## 返回值

返回值为 [IntersectionObserver](https://opendocs.alipay.com/mini/api/intersectionobserver-overview) 对象实例。
