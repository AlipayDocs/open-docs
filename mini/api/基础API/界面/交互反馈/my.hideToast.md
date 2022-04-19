# 简介

**my.hideToast** 是隐藏弱提示的 API。

## 使用限制

此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验

![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/e9f3b3c8c7c3cd7d169955c9facf59fa.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=none&width=127)

# 接口调用

## Herbox

[小程序在线](https://herbox-embed.alipay.com/s/doc-toast?theme=light&previewZoom=75&chInfo=openhome-doc) 

## 示例代码

### .json 示例代码
```json
{
    "defaultTitle": "Toast"
}
```

### .axml 示例代码
```html
<!-- API-DEMO page/API/toast/toast.axml-->
<view class="page">
  <view class="page-description">Toast API</view>
  <view class="page-section">
    <view class="page-section-title">my.showToast</view>
    <view class="page-section-btns">
      <view type="primary" onTap="showToastSuccess">显示 success 提示</view>
      <view type="primary" onTap="showToastFail">显示 fail 提示</view>
    </view>
    <view class="page-section-btns">
      <view type="primary" onTap="showToastException">显示 exception 提示</view>
      <view type="primary" onTap="showToastNone">显示 none 弱提示</view>
    </view>
  </view>
  <view class="page-section">
    <view class="page-section-title">my.hideToast</view>
    <view class="page-section-btns">
      <view onTap="hideToast">隐藏弱提示</view>
    </view>
  </view>
</view>
```

### .js 示例代码
```javascript
// API-DEMO page/API/toast/toast.js
Page({
  showToastSuccess() {
    my.showToast({
      type: 'success',
      content: '操作成功',
      duration: 3000,
      success: () => {
        my.alert({
          title: 'toast 消失了',
        });
      },
    });
  },
  showToastFail() {
    my.showToast({
      type: 'fail',
      content: '操作失败',
      duration: 3000,
      success: () => {
        my.alert({
          title: 'toast 消失了',
        });
      },
    });
  },
  showToastException() {
    my.showToast({
      type: 'exception',
      content: '网络异常',
      duration: 3000,
      success: () => {
        my.alert({
          title: 'toast 消失了',
        });
      },
    });
  },
  showToastNone() {
    my.showToast({
      type: 'none',
      content: '提醒',
      duration: 3000,
      success: () => {
        my.alert({
          title: 'toast 消失了',
        });
      },
    });
  },
  hideToast() {
    my.hideToast()
  },
})
```

## 入参

Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| success | Function | 否 | 接口调用成功的回调函数。 |
| fail | Function | 否 | 接口调用失败的回调函数。 |
| complete | Function | 否 | 接口调用结束的回调函数（调用成功、失败都会执行）。 |

