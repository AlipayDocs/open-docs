# 简介

**my.setKeepScreenOn** 是设置是否保持屏幕长亮状态的 API。仅在当前小程序生效，离开小程序后失效。

## 使用限制

- 基础库 [1.3.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.8 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验

![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/36116125389be0190f5b4e446bfc93fa.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=stroke&width=127)

## 效果示例

![|300x540](https://gw.alipayobjects.com/zos/skylark-tools/public/files/57ac70ca95c208105f2456c578533fbc.gif#align=left&display=inline&height=540&margin=%5Bobject%20Object%5D&originHeight=540&originWidth=300&status=done&style=stroke&width=300)

# 接口调用

## 示例代码

### .axml 示例代码

```html
<!-- API-DEMO page/API/screen/screen.axml-->
<view class="page">
  <view class="page-description">屏幕亮度 API</view>
  <view class="page-section">
    <view class="page-section-title">设置是否保持屏幕长亮状态</view>
    <view class="page-section-demo">
      <switch checked="{{status}}" onChange="switchKeepScreenOn" />
    </view>
  </view>
  <view class="page-section">
    <view class="page-section-title">设置屏幕亮度</view>
    <view class="page-section-demo">
      <slider
        value="{{brightness}}"
        max="1"
        min="0"
        onChange="sliderChange"
        step="0.02"
      />
    </view>
  </view>
  <view class="page-section">
    <view class="page-section-title">获取屏幕亮度</view>
    <view class="page-section-demo">
      <button type="primary" onTap="getBrightness">获取屏幕亮度</button>
    </view>
  </view>
</view>
```

### .js 示例代码

```javascript
// API-DEMO page/API/screen/screen.js
Page({
  data: {
    status: false,
    brightness: 1,
  },
  onLoad() {
    my.getScreenBrightness({
      success: res => {
        this.setData({
          brightness: res.brightness,
        });
      },
    });
  },
  sliderChange(e) {
    my.setScreenBrightness({
      brightness: e.detail.value,
      success: res => {
        this.setData({
          brightness: e.detail.value,
        });
      },
    });
  },
  switchKeepScreenOn(e) {
    my.setKeepScreenOn({
      keepScreenOn: e.detail.value,
      success: res => {
        this.setData({
          status: e.detail.value,
        });
      },
    });
  },
  getBrightness() {
    my.getScreenBrightness({
      success: res => {
        my.alert({
          content: `当前屏幕亮度：${res.brightness}`,
        });
      },
    });
  },
});
```

## 入参

Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| keepScreenOn | Boolean | 是 | 是否保持屏幕长亮状态。 |
| success | Function | 否 | 接口调用成功的回调函数。 |
| fail | Function | 否 | 接口调用失败的回调函数。 |
| complete | Function | 否 | 接口调用结束的回调函数（调用成功、失败都会执行）。 |

## Bug & Tip

由于 chooseCity 、chooseVideo 等功能会唤起小程序外部的组件页面，因此 my.setKeepScreenOn 会在这类组件页面中失效，当关闭组件回到小程序后 my.setKeepScreenOn 会继续生效


