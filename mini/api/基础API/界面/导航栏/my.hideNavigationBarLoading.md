# 简介

**my.hideNavigationBarLoading** 是在当前页面隐藏导航条的加载动画的 API。

## 使用限制

此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验

![|127x157](https://mdn.alipayobjects.com/afts/img/A*FbIjSbhTHgQAAAAAAAAAAABkAa8wAA/original?bz=openpt_doc&t=PSGk17o4wJtGbKewpCXyfAAAAABkMK8AAAAA#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=none&width=127)

# 接口调用

## 在线示例

[小程序在线](https://opendocs.alipay.com/openbox/mini/opendocs/navigation-bar-loading?view=preview&defaultPage=pages/index/index&defaultOpenedFiles=pages/index/index&theme=light)

### .js 示例代码

```javascript
Page({
  showNavigationBarLoading() {
    my.showNavigationBarLoading();
  },
  hideNavigationBarLoading() {
    my.hideNavigationBarLoading();
  },
});
```
