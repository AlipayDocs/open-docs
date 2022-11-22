# 简介

**my.offLocatedComplete** 是取消监听地理位置定位完成事件的 API，只针对 [my.chooseCity](https://opendocs.alipay.com/mini/api/ui-city) 中属性 setLocatedCity 为 true 的情况。

推荐使用接口 [ChooseCityTask](https://opendocs.alipay.com/mini/04naqz) 替代 my.offLocatedComplete。

## 使用限制

- 基础库 [2.7.0](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- IDE 模拟器暂不支持调试，请以真机调试结果为准。
- 此 API 暂仅支持企业支付宝小程序使用。

# 接口调用

## 示例代码

### .axml 示例代码

```html
<!-- API-DEMO page/API/choose-city/choose-city.axml-->
<view class="page">
  <view class="page-description">选择城市 API</view>
  <view class="page-section">
    <view class="page-section-title">my.chooseCity</view>
    <view class="page-section-demo">
      <button type="primary" onTap="chooseCity">选择城市</button>
    </view>
  </view>
  <view class="page-description">修改当前定位城市的名称 API</view>
  <view class="page-section">
    <view class="page-section-title">my.setLocatedCity</view>
    <view class="page-section-demo">
      <button type="primary" onTap="setLocatedCity">
        修改当前定位城市的名称
      </button>
    </view>
  </view>
</view>
```

### .js 示例代码

```javascript
// API-DEMO page/choose-city/choose-city.js
Page({
  onLoad() {
    this.locatedCompleteHandler = function (result) {
      my.setLocatedCity({
        locatedCityId: result.locatedCityId,
        locatedCityName: '修改后的城市名',
        success: res => {
          my.alert({ content: '修改当前定位城市成功' + JSON.stringify(res) });
        },
        fail: error => {
          my.alert({ content: '修改当前定位城市失败' + JSON.stringify(error) });
        },
      });
    };
  },
  onUnload() {
    if (my.canIUse('offLocatedComplete')) {
      my.offLocatedComplete(this.locatedCompleteHandler);
    }
  },
  chooseCity() {
    my.onLocatedComplete(this.locatedCompleteHandler);
    my.chooseCity({
      showLocatedCity: true,
      showHotCities: true,
      success: res => {
        my.alert({
          title: 'chooseCity response: ' + JSON.stringify(res),
        });
      },
    });
  },
  setLocatedCity() {
    my.chooseCity({
      showLocatedCity: true,
      showHotCities: true,
      setLocatedCity: true,
      success: res => {
        my.alert({
          title: 'chooseCity response: ' + JSON.stringify(res),
        });
      },
    });
  },
});
```

## 入参

入参为回调函数：

| **参数** | **类型** | **描述**                         |
| -------- | -------- | -------------------------------- |
| callback | Function | 地理位置定位完成事件的回调函数。 |
