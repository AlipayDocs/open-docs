
# 简介
**my.alert** 是警告框 API，可以设置警告框的标题、内容、按钮文字等。

## 使用限制

- 暂不支持设置图片等样式。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验

![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/34912116506eb06e4f55f825b4ff9120.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=none&width=127)

# 接口调用

## Herbox

[小程序在线](https://herbox-embed.alipay.com/s/doc-alert?theme=light&previewZoom=75&chInfo=openhome-doc) 

## 示例代码

### .json 示例代码
```json
{
  "defaultTitle": "Alert"
}
```

### .axml 示例代码
```html
<!-- API-DEMO page/API/alert/alert.axml-->
<view class="page">
  <view class="page-description">警告框 API</view>
  <view class="page-section">
    <view class="page-section-title">my.alert</view>
    <view class="page-section-demo">
      <button type="primary" onTap="alert">显示警告框</button>
    </view>
  </view>
</view>
```

### .js 示例代码
```javascript
// API-DEMO page/API/alert/alert.js
Page({
  alert() {
    my.alert({
      title: '亲',
      content: '您本月的账单已出',
      buttonText: '我知道了',
      success: () => {
        my.alert({
          title: '用户点击了「我知道了」',
        });
      }
    });
  },
})
```

## 入参
Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| title | String | 否 | 警告框的标题。 |
| content | String | 否 | 警告框的内容。 |
| buttonText | String | 否 | 按钮文字，默认为 **确定**。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

