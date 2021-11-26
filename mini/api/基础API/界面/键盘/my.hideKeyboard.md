
# 简介
**my.hideKeyboard** 是隐藏键盘的 API。

## 使用限制
此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验
![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/86eaf0743ce03460b76ef72693f497f2.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=stroke&width=127)

## 效果示例
![|723x407](https://gw.alipayobjects.com/zos/skylark-tools/public/files/3cd50c1a6fef117e228bba9efd495c15.png#align=left&display=inline&height=420&margin=%5Bobject%20Object%5D&originHeight=720&originWidth=1280&status=done&style=stroke&width=746)

# 接口调用

## 示例代码
```json
// API-DEMO page/API/keyboard/keyboard.json
{
  "defaultTitle": "键盘"
}
```
```html
<!-- API-DEMO page/API/keyboard/keyboard.axml-->
<view class="page">
  <view class="page-description">输入框</view>
  <view class="page-section">
    <view class="form-row">
      <view class="form-row-label">密码键盘</view>
      <view class="form-row-content">
        <input class="input" password type="text" onInput="bindHideKeyboard" placeholder="输入 123 自动收起键盘" />
      </view>
    </view>
    <view class="form-row">
      <view class="form-row-label">数字键盘</view>
      <view class="form-row-content">
        <input class="input" type="digit" onInput="bindHideKeyboard" placeholder="输入 123 自动收起键盘" />
      </view>
    </view>
  </view>
</view>
```
```javascript
// API-DEMO page/API/keyboard/keyboard.js
Page({
  bindHideKeyboard(e) {
    if (e.detail.value === "123") {
      // 收起键盘
      my.hideKeyboard();
    }
  },
});
```
