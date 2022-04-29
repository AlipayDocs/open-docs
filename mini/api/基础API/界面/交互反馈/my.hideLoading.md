# 简介

**my.hideLoading** 是隐藏加载提示的过渡效果的 API，可与 [my.showLoading](https://opendocs.alipay.com/mini/006l2f) 配合使用。

## 使用限制

此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例

[小程序在线](https://opendocs.alipay.com/examples/f82160bc-7215-4979-b377-0d8c2b32d5cf) 

### .js 示例代码
```javascript
// .js
Page({
  onLoad() {
    my.showLoading();
    const that = this;
    setTimeout(() => {
      my.hideLoading({
        page: that,  // 防止执行时已经切换到其它页面，page 指向不准确
      });
    }, 4000);
  }
})
```

## 入参
Object 类型，参数如下：

