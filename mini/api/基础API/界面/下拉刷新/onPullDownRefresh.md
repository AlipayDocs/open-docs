# 简介
**onPullDownRefresh** 是用于在 Page 中自定义 onPullDownRefresh 函数，可以监听该页面的下拉刷新事件。

调用 [my.startPullDownRefresh](https://opendocs.alipay.com/mini/api/ui-pulldown) 后触发下拉刷新动画，然后会触发 onPullDownRefresh 监听方法，效果与用户手动下拉刷新一致。但 **my.startPullDownRefresh** 不受 onPullDownRefresh 的 `allowsBounceVertical` 、`pullRefresh` 参数影响。

## 使用限制

- 需要在 app.json 的 window 选项中配置 `"allowsBounceVertical":"YES"`，在页面对应的 .json 配置文件中配置 `"pullRefresh":true` 选项，才可开启页面下拉刷新事件。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验

![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/bd8dbb40d62dd58710fa54c9fc6ea7af.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=none&width=127)

# 接口调用

## 示例

[小程序在线](https://opendocs.alipay.com/examples/0fe7dc2d-60c9-438c-a221-cf9b43274af1) 

### .json 示例代码
在页面对应的 .json 文件中添加如下配置：
```json
{
  "defaultTitle": "下拉刷新",
  "pullRefresh": true
}
```
在 app.json 文件中添加如下配置：
```json
{
  "window": {
    "allowsBounceVertical": "YES"
  }
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
  onPullDownRefresh() {
    console.log('onPullDownRefresh', new Date());
  },
  stopPullDownRefresh() {
    my.stopPullDownRefresh({
      complete(res) {
        console.log(res, new Date())
      }
    })
  }
});
```

## 配置

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| pullRefresh | Boolean | 否 | 是否允许下拉刷新。<br />Android 端默认值是 true，iOS 端默认值是 false。<br />**说明**：下拉刷新生效的前提是 allowsBounceVertical 值为 `YES` 。 |
| allowsBounceVertical | String | 否 | 页面是否支持纵向拽拉超出实际内容。默认 YES，支持 `YES`/`NO`。 |
