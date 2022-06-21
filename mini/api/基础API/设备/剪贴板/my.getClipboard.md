**注意**：本接口功能可能涉及隐私问题，请谨慎使用。 

# 简介
**my.getClipboard** 获取剪贴板数据。

## 使用限制
此 API 暂仅支持企业支付宝账户使用。

## 扫码体验

![](https://gw.alipayobjects.com/zos/skylark-tools/public/files/af4df1405eda32780191e6123cf5870d.jpeg#align=left&display=inline&height=158&margin=%5Bobject%20Object%5D&originHeight=158&originWidth=128&status=done&style=stroke&width=128)

## 效果示例

![](https://gw.alipayobjects.com/zos/skylark-tools/public/files/0d774501f4c262f429ecca3226ce673a.gif#align=left&display=inline&height=540&margin=%5Bobject%20Object%5D&originHeight=540&originWidth=300&status=done&style=stroke&width=300)

# 接口调用

## 示例代码

### .json 示例代码

```json
// API-DEMO page/API/clipboard/clipboard.json
{
  "defaultTitle": "Clipboard"
}
```

### .axml 示例代码
```html
<!-- API-DEMO page/API/clipboard/clipboard.axml-->
<view class="page">
  <view class="page-section">
    <view class="page-section-title">setClipboard</view>
    <view class="page-section-demo">
      <input onInput="handleInput" value="{{text}}" />
      <button class="clipboard-button" type="primary" size="mini" onTap="handleCopy">复制</button>
    </view>
  </view>
  <view class="page-section">
    <view class="page-section-title">getClipboard</view>
    <view class="page-section-demo">
      <input onInput="bindInput" value="{{copy}}" disabled />
      <button class="clipboard-button" type="default" size="mini" onTap="handlePaste">粘贴</button>
    </view>
  </view>
</view>
```

### .js 示例代码
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

### .acss 示例代码
```css
/* API-DEMO page/API/clipboard/clipboard.acss */
.clipboard-button {
  margin-left: 5px;
}
```

# 入参
Object 类型，属性如下：

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |


## success 回调函数

入参为 Object 类型，属性如下：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| text | String | 剪贴板数据。 |
