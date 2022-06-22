# 简介
**my.pageScrollTo** 是滚动到页面的目标位置的 API。支持滚动距离和选择器两种方式定位，滚动距离优先级高于选择器。

## 使用限制
此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验
![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/fddf26af471fde54223b5c44dc7e772d.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=none&width=127)

# 接口调用

## 示例

[小程序在线](https://opendocs.alipay.com/examples/d751a633-ea1a-4f39-b297-cd688e30e3c9) 

### .axml 示例代码
```html
<!-- API-DEMO page/API/page-scroll-to/page-scroll-to.axml-->
<view class="page">
  <view class="page-description">页面滚动 API</view>
  <view class="page-section">
    <view class="page-section-title">
      my.pageScrollTo
    </view>
    <view class="page-section-demo">
      <input type="text" placeholder="key" name="key" value="{{scrollTop}}" onInput="scrollTopChange"></input>
    </view>
    <view class="page-section-btns">
      <view onTap="scrollTo">页面滚动</view>
    </view>
  </view>
  <view style="height:1000px"/>
</view>
```

### .js 示例代码
```javascript
// API-DEMO page/API/page-scroll-to/page-scroll-to.js
Page({
  data: {
    scrollTop: 0,
  },
  scrollTopChange(e) {
    this.setData({
      scrollTop: e.detail.value,
    });
  },
  onPageScroll({ scrollTop }) {
    console.log('onPageScroll', scrollTop);
  },
  scrollTo() {
    my.pageScrollTo({
      scrollTop: parseInt(this.data.scrollTop),
      duration: 300,
    });
  },
});
```

## 入参
为 Object  类型，属性如下：

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| scrollTop | Number | 否 | 滚动到页面的目标位置，单位为 px。|
| duration | Number | 否 | 滚动动画的时长，单位为 ms（毫秒）。默认值为 0。<br />基础库 1.20.0 或更高版本开始支持。 |
| selector | String | 否 | CSS 选择器。<br />基础库 1.20.0 或更高版本开始支持。 |
| success | Function | 否 | 接口调用成功的回调函数。 |
| fail | Function | 否 | 接口调用失败的回调函数。 |
| complete | Function | 否 | 接口调用结束的回调函数（调用成功、失败都会执行）。 |

### selector 语法
当传入 selector 参数，框架会执行 document.querySelector(selector) 以选取目标节点，支持标准的 CSS 选择器语法。

# 常见问题 FAQ

## Q：为什么调用 my.pageScrollTo 页面没有滚动？
A：请确认下滚动行为是否是 scroll-view 等组件内发生的，my.pageScrollTo 是页面滚动的 API。

## Q：my.pageScrollTo 支持跨自定义组件的后代选择器吗？
A：目前 my.pageScrollTo 只支持标准的 CSS 选择器。
