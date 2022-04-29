# 简介
**my.showLoading** 是显示加载提示的过渡效果的 API，可与 [my.hideLoading](https://opendocs.alipay.com/mini/api/nzf540) 配合使用。

## 使用限制
此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验

![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/9b97b37bc6021ac42b6772643f2b62ad.png#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=none&width=127)

# 接口调用

## 示例

[小程序在线](https://opendocs.alipay.com/examples/3c03908e-51e5-4a4a-bca3-2800a317c0a5) 

### .json 示例代码

```json
{
  "defaultTitle": "加载提示"
}
```

### .axml 示例代码
```html
<!-- API-DEMO page/API/loading/loading.axml-->
<view class="page">
  <view class="page-section">
    <view class="page-section-title">
      显示 loading 后，会覆盖整个h5页面，页面元素不能交互。
    </view>
    <view class="page-section-btns">
      <view onTap="showLoading">显示加载提示</view>
    </view>
  </view>
</view>
```

### .js 示例代码

```javascript
// API-DEMO page/API/loading/loading.js
Page({
  showLoading() {
    my.showLoading({
      content: '加载中...',
      delay: 1000,
    });
    setTimeout(() => {
      my.hideLoading();
    }, 5000);
  },
});
```

### .acss 示例代码

```css
/* API-DEMO page/API/loading/loading.acss */
.tips{
  margin-left: 10px;
  margin-top: 20px; 
  color: red;
  font-size: 12px;
}
.tips .item {
  margin: 5px 0;
  color: #888888;
  line-height: 14px;
}
```

## 入参
Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| content | String | 否 | 提示中的文字内容。 |
| delay | Number | 否 | 延迟显示，单位为毫秒（ms），默认值为 0。<br />如果在此时间之前调用了 **my.hideLoading** 则不会显示。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |
