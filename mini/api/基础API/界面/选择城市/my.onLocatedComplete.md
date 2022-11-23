# 简介

**my.onLocatedComplete** 是监听地理位置定位完成事件的 API，只针对 [my.chooseCity](https://opendocs.alipay.com/mini/api/ui-city) 中属性 setLocatedCity 为 true 的情况。

推荐使用 my.chooseCity 所返回 [ChooseCityTask](https://opendocs.alipay.com/mini/04naqz) 的 onLocatedComplete 方法替代 my.onLocatedComplete。

## 使用限制

- IDE 模拟器暂不支持调试，请以真机调试结果为准。
- 此 API 暂仅支持企业支付宝小程序使用。

## 扫码体验

![|127x157](https://mdn.alipayobjects.com/afts/img/A*uGCmRImDNksq0wpOl9aflwBkAa8wAA/original?bz=openpt_doc&t=2sNXA_LmBkuW7-CwiT-HUAAAAABkMK8AAAAA#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=none&width=127)

# 接口调用

## 示例

[小程序在线](https://opendocs.alipay.com/openbox/mini/opendocs/choose-city?view=preview&defaultPage=pages/index/index&defaultOpenedFiles=pages/index/index&theme=light)

### .js 示例代码

```javascript
// API-DEMO page/choose-city/choose-city.js
Page({
  chooseCity() {
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
    my.onLocatedComplete(function (result) {
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
    });
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

## 返回示例

### 回调函数返回示例

地理位置定位完成时，触发回调函数，回调参数示例如下：

```javascript
{
  longitude: 100.3,
  latitude: 30.1,
  locatedCityId: "",
};
```

## 入参

入参为回调函数：

| **参数** | **类型** | **描述**                               |
| -------- | -------- | -------------------------------------- |
| 回调函数 | Function | 小程序地理位置定位完成事件的回调函数。 |

### 回调函数

回调函数会携带一个 Object 类型的对象，其属性如下：

| **属性**      | **类型** | **描述**                                     |
| ------------- | -------- | -------------------------------------------- |
| longitude     | Number   | 当前定位城市经度。                           |
| latitude      | Number   | 当前定位城市经度。                           |
| locatedCityId | String   | 当前定位城市 id，setLocatedCity 的时候带上。 |
