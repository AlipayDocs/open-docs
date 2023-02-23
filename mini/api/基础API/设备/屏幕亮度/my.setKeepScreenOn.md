# 简介

**my.setKeepScreenOn** 设置是否保持屏幕常亮。

常亮设置仅对当前小程序生效，离开小程序后自动失效。


## 使用限制

- 基础库 [1.3.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.8 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验

![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/36116125389be0190f5b4e446bfc93fa.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=stroke&width=127)

# 接口调用

## 示例代码

### .axml 示例代码
```html
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
| keepScreenOn | Boolean | 是 | 是否保持屏幕常亮状态。 |
| success | Function | 否 | 接口调用成功的回调函数。 |
| fail | Function | 否 | 接口调用失败的回调函数。 |
| complete | Function | 否 | 接口调用结束的回调函数（调用成功、失败都会执行）。 |

## Bug & Tip

* my.chooseCity、my.chooseVideo 等 API 会唤起外部的组件页面，因而会暂时解除 my.setKeepScreenOn 设置的常亮状态，当关闭这类组件页面返回到小程序后，之前设置的常亮状态会恢复。


