# 简介

**my.getClipboard** 是获取剪贴板数据的 API。

**注意**：使用本接口功能可能涉及隐私问题，请谨慎使用。

## 使用限制

此 API 暂仅支持企业支付宝小程序使用。

## 扫码体验

![](https://gw.alipayobjects.com/zos/skylark-tools/public/files/af4df1405eda32780191e6123cf5870d.jpeg#align=left&display=inline&height=158&margin=%5Bobject%20Object%5D&originHeight=158&originWidth=128&status=done&style=stroke&width=128)

## 效果示例

![](https://gw.alipayobjects.com/zos/skylark-tools/public/files/0d774501f4c262f429ecca3226ce673a.gif#align=left&display=inline&height=540&margin=%5Bobject%20Object%5D&originHeight=540&originWidth=300&status=done&style=stroke&width=300)

# 接口调用

## 示例代码

**.js 示例代码**

```javascript
// API-DEMO page/API/clipboard/clipboard.js
Page({
  data: {
    text: '3.1415926',
    copy: '',
  },
  handleInput(e) {
    this.setData({
      text: e.detail.value,
    });
  },
  handleCopy() {
    my.setClipboard({
      text: this.data.text,
    });
  },
  handlePaste() {
    my.getClipboard({
      success: ({ text }) => {
        this.setData({ copy: text });
      },
    });
  },
});
```

**.axml 示例代码**

```html
<!-- API-DEMO page/API/clipboard/clipboard.axml-->
<view class="page">
  <view class="page-section">
    <view class="page-section-title">setClipboard</view>
    <view class="page-section-demo">
      <input onInput="handleInput" value="{{text}}" />
      <button
        class="clipboard-button"
        type="primary"
        size="mini"
        onTap="handleCopy"
      >
        复制
      </button>
    </view>
  </view>
  <view class="page-section">
    <view class="page-section-title">getClipboard</view>
    <view class="page-section-demo">
      <input onInput="bindInput" value="{{copy}}" disabled />
      <button
        class="clipboard-button"
        type="default"
        size="mini"
        onTap="handlePaste"
      >
        粘贴
      </button>
    </view>
  </view>
</view>
```

## 入参

Object 类型，属性如下：

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

## 出参

success 回调收到 Object 类型的参数，属性如下：

| **属性** | **类型** | **描述**     |
| -------- | -------- | ------------ |
| text     | String   | 剪贴板数据。 |

## 错误码

fail 回调收到 Object 类型的参数，error 属性为错误码：

| **error** |  **描述** | **说明** | **解决方案** | 
| --- | --- | --- | --- | 
| 2001   |  用户不允许授权。   | 用户拒绝为当前小程序授权剪贴板功能。        | 请在交互设计中考虑这种情况。  |
| 2003   |  用户勾选了不允许授权选项。    | 用户拒绝授权，并且此次勾选了总是保持拒绝。  | 如有必要，可提醒用户手动授权：小程序右上角胶囊按钮 -> 设置 -> 剪贴板，或者调用 [my.openSetting](https://opendocs.alipay.com/mini/api/qflu8f) 帮用户打开该设置页面。 |
| 2002   |  用户不允许授权。    | 用户此前已经拒绝授权且勾选了总是保持拒绝，此次调用直接失败。 | 如有必要，可提醒用户手动授权：小程序右上角胶囊按钮 -> 设置 -> 剪贴板，或者调用 [my.openSetting](https://opendocs.alipay.com/mini/api/qflu8f) 帮用户打开该设置页面。 |
| 2004 |  用户不允许授权。 | iOS 16 版本对读取取剪切内容组件有更新，出于对用户体验考虑，支付宝对小程序暂时禁用了读取剪贴板功能，调用此 API 会直接报这个错，并非一般意义上的“用户不允许授权”。 | 请确保小程序对自动读取剪贴板能力没有强依赖。支付宝小程序开发人员正在快马加鞭改造中，等后续开放公告。 | 
