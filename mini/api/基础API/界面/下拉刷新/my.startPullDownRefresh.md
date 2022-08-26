# 简介

**my.startPullDownRefresh** 是主动开启下拉刷新的 API。

调用 my.startPullDownRefresh 后触发下拉刷新动画，效果与用户手动下拉刷新一致（会触发 [onPullDownRefresh](https://opendocs.alipay.com/mini/api/wo21qk) 监听方法）。

当处理完数据刷新后，[my.stopPullDownRefresh](https://opendocs.alipay.com/mini/api/pmhkbb) 可停止当前页面的下拉刷新。

## 使用限制

- 本接口不受 **onPullDownRefresh** 的 `allowsBounceVertical` 、`pullRefresh` 参数影响。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验

![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/b6870cc16df411396f0c4fee0e518d6e.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=none&width=127)

# 接口调用

## 在线示例

[小程序在线](https://opendocs.alipay.com/openbox/mini/opendocs/pull-down-refresh?view=preview&defaultPage=pages/index/index&defaultOpenedFiles=pages/index/index&theme=light)

### .json 示例代码

```json
{
  "defaultTitle": "下拉刷新",
  "pullRefresh": true
}
```

### .axml 示例代码

```html
<!-- API-DEMO page/API/pull-down-refresh/pull-down-refresh.axml-->
<view class="page">
  <view class="page-section">
    <view class="page-section-title">下滑页面即可刷新</view>
    <view class="page-section-btns">
      <view type="primary" onTap="stopPullDownRefresh">停止刷新</view>
    </view>
  </view>
</view>
```

### .js 示例代码

```javascript
// API-DEMO page/API/pull-down-refresh/pull-down-refresh.js
Page({
  //根据业务需要主动调用接口下拉刷新
  pullDown() {
    my.startPullDownRefresh();
  },
  onPullDownRefresh() {
    console.log('onPullDownRefresh', new Date());
  },
  stopPullDownRefresh() {
    my.stopPullDownRefresh({
      complete(res) {
        console.log(res, new Date());
      },
    });
  },
});
```

## 入参

Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| success | Function | 否 | 接口调用成功的回调函数。 |
| fail | Function | 否 | 接口调用失败的回调函数。 |
| complete | Function | 否 | 接口调用结束的回调函数（调用成功、失败都会执行）。 |
