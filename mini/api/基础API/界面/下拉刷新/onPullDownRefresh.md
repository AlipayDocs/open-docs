# 简介
**onPullDownRefresh** 可以监听该页面的用户下拉刷新事件。

需要在 app.json 的 window 选项中配置 `"allowsBounceVertical": "YES"`，并且在页面对应的 .json 文件中配置 `"pullRefresh": true`，当前页面才允许下拉刷新。

可以调用 [my.startPullDownRefresh](https://opendocs.alipay.com/mini/api/ui-pulldown) 主动触发下拉刷新，调用后触发下拉刷新动画，效果与用户手动下拉刷新一致，可以触发 onPullDownRefresh 事件监听。但 **my.startPullDownRefresh** 不受 onPullDownRefresh 的 `allowsBounceVertical` 、`pullRefresh` 参数影响。

调用 [my.stopPullDownRefresh](https://opendocs.alipay.com/mini/api/pmhkbb) 可以停止当前页面的下拉刷新。

## 使用限制

此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验

![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/bd8dbb40d62dd58710fa54c9fc6ea7af.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=none&width=127)

# 接口调用

## 在线示例

[小程序在线](https://opendocs.alipay.com/openbox/mini/opendocs/pull-down-refresh?view=preview&defaultPage=pages/index/index&defaultOpenedFiles=pages/index/index&theme=light) 

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
| pullRefresh | Boolean | 否 | 是否允许下拉刷新。<br />默认值是 false。<br />**说明**：下拉刷新生效的前提是 allowsBounceVertical 值为 `YES` 。 |
| allowsBounceVertical | String | 否 | 页面是否支持纵向拽拉超出实际内容。默认 YES，支持 `YES`/`NO`。 |

# 常见问题

## Q：为什么 onPullDownRefresh 回调不触发？
A：需要在用户主动下拉刷新或者调用 my.startPullDownRefresh 后才会触发 onPullDownRefresh 回调，如果是用户主动下拉刷新，需要在 app.json 中设置 allowsBounceVertical: 'YES', 在页面的 json 文件中设置 pullRefresh: true。
