# 简介

页面属性配置节点，用于指定页面的一些属性、监听页面事件。只能是页面内的第一个节点。通过这个节点可以获得类似于调用 [my.setBackgroundTextStyle](https://opendocs.alipay.com/mini/api/aamqae)、[my.setBackgroundColor](https://opendocs.alipay.com/mini/api/set-background) 等接口调用的效果。

## 使用限制

版本要求基础库 [2.7.7](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 及以上，若版本较低，建议做 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。

# 使用

## 示例代码

### .axml 示例代码

```html
<page-meta
  background-text-style="{{bgTextStyle}}"
  background-color="{{bgColor}}"
  background-color-top="{{bgColorTop}}"
  background-color-bottom="{{bgColorBottom}}"
  scroll-top="{{scrollTop}}"
  page-style="color: green"
  root-font-size="16px"
  onScroll="handleScroll"
>
</page-meta>
```

### .js 示例代码

```javascript
Page({
  data: {
    scrollTop: '200rpx',
    bgColor: '#ff0000',
    bgColorTop: '#00ff00',
    bgColorBottom: '#0000ff',
    nbTitle: '标题',
    nbLoading: false,
    nbFrontColor: '#000000',
    nbBackgroundColor: '#ffffff',
  },
  handleScroll(event) {
    const { scrollTop } = event.detail;
    console.log(scrollTop);
  },
});
```

## 属性说明

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| background-color | String | 窗口的背景色，必须为十六进制颜色值。 |
| background-color-top | String | 顶部窗口的背景色，必须为十六进制颜色值，仅 iOS 支持。 |
| background-color-bottom | String | 底部窗口的背景色，必须为十六进制颜色值，仅 iOS 支持。 |
| root-background-color | String | 页面内容的背景色，用于页面中的空白部分和页面大小变化 resize 动画期间的临时空闲区域。 |
| scroll-top | String | 滚动位置，可以使用 px 或者 rpx 为单位，在被设置时，页面会滚动到对应位置。 |
| scroll-duration | Number | 滚动动画时长。<br />**默认值：** 300 |
| page-style | String | 页面根节点样式，页面根节点是所有页面节点的祖先节点，相当于 HTML 中的 body 节点。 |
| page-font-size | String | 页面 page 的字体大小，可以设置为`system`，表示使用当前用户设置的支付宝字体大小。 |
| root-font-size | String | 页面的根字体大小，页面中的所有 rem 单位，将使用这个字体大小作为参考值，即 `1rem` 等于这个字体大小；<br />可以设置为 `system`，表示使用当前用户设置的支付宝字体大小。 |
| onScroll | EventHandle | 页面滚动时触发，`event.detail = { scrollTop }` |
