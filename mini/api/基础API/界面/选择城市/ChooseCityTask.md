# 简介
一个可以监听地理位置定位完成事件，以及修改默认定位城市名称的对象。

## 使用限制

- 基础库 [2.8.0](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2)、客户端 10.2.70 开始支持，低版本需要做 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- [my.chooseCity](https://opendocs.alipay.com/mini/api/ui-city) 入参 `showLocatedCity` 和 `setLocatedCity` 需同时设置为 `true`，`ChooseCityTask.onLocatedComplete` 才会触发。
- 此 API 暂仅支持企业支付宝小程序使用。

# 方法

## ChooseCityTask.onLocatedComplete

### 功能描述
监听地理位置定位完成事件。

### 入参
**function callback**<br />地理位置定位完成事件的回调函数。

#### **callback **参数
**Object res**

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| longitude | Number | 当前定位城市经度。 |
| latitude | Number | 当前定位城市经度。 |


## ChooseCityTask.offLocatedComplete

### 功能描述
取消监听地理位置定位完成事件。

### 入参
**function callback**<br />地理位置定位完成事件的回调函数。

## ChooseCityTask.setLocatedCity

### 功能描述
修改默认定位城市的名称。

### 入参
**Object res**

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| locatedCityName | String | 是 | 当前定位城市的名称。 |
| locatedCityAdCode | String | 否 | 当前定位城市的行政区划代码，不传值时以控件默认拿到的为准。 |
| locatedCityPinyin | String | 否 | 当前定位城市的拼音，不传值时以控件默认拿到的为准。 |


## 示例代码
```typescript

const chooseCityTask = my.chooseCity({
  // 是否显示当前定位城市
  showLocatedCity: true,
  showHotCities: true,
  // 是否修改当前定位城市
  setLocatedCity: true,
  success: (res) => {
    my.alert({ title: `chooseCity: ${JSON.stringify(res)}` })
  },
  fail: (error) => {
    my.alert({ content: `选择失败${JSON.stringify(error)}` })
  },
  complete: () => {
    my.showToast({ content: 'complete回调' })
  },
});

const onLocatedCompleteCallback = (locatedCompleteRes => {
  const { longitude, latitude } = locatedCompleteRes;
  // 根据经纬度反查出正确的城市名
  chooseCityTask.setLocatedCity({
    locatedCityName: 'new cityname', // 修改默认定位城市名
    sucess() {
      console.log('修改成功');
    },
    fail() {
      console.log('修改失败');
    },
    complete() {
      chooseCityTask.offLocatedComplete(onLocatedCompleteCallback);
    }
  });
});

chooseCityTask.onLocatedComplete(onLocatedCompleteCallback);
```
