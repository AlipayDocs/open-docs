支付宝小程序为开发者提供了丰富的 [小程序 API](https://opendocs.alipay.com/mini/api) ，开发者可方便快捷地调用这些 API 完成相关任务。

小程序前端 API 包括基础、应用级事件、界面、多媒体、缓存、文件、位置、网络、设备、数据安全、分享、自定义通用菜单、更新管理、web-view 组件控制、升级支付宝最新版本、开放能力（基础能力、支付能力、资金能力、会员能力、营销能力、安全能力）等多个大类。

其中，小程序前端 API 分为两大类：事件监听 API、功能 API。

# 事件监听 API

事件监听型 API 以 `my.on` 开头，用于监听某个系统事件是否触发。 事件监听型 API 接受一个 callback 回调函数作为参数。当具体事件触发时，会触发 callback 函数调用。该 callback 函数可以传给对应以 `my.off` 开头的同名 API 来解除监听关系，如果直接调用以 `my.off` 开头的同名 API 则解除所有监听关系。 以监听低功耗蓝牙设备的特征值变化的事件 API [my.onBLECharacteristicValueChange](https://opendocs.alipay.com/mini/api/cdu501) 为例：

```javascript
Page({
  onLoad() {
    this.callback = this.callback.bind(this);
    my.onBLECharacteristicValueChange(this.callback);
  },
  onUnload() {
    // 页面卸载时解除某个监听
    my.offBLECharacteristicValueChange(this.callback);
    // 或者解除所有监听
    // my.offBLECharacteristicValueChange();
  },
  callback(res) {
    console.log(res);
  },
});
```

# 功能 API

功能型 API 是不以 `my.on` 或 `my.off` 开头的 API，用于实现某个特定功能。功能型 API 可分为异步型 API 和同步型 API。

## 异步型功能 API

大部分 API 都是异步型功能 API，例如 [my.navigateTo](https://opendocs.alipay.com/mini/api/zwi8gx)、[my.request](https://opendocs.alipay.com/mini/api/owycmh)。异步型功能 API 的入参都为一个 Object 对象，并包含三个子属性：

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

回调结果若无特殊说明，一般为一个 Object 对象，包含以下子属性：

| **属性** | **类型** | **说明**                             |
| -------- | -------- | ------------------------------------ |
| error  | Number   | 错误码，接口调用失败时返回，一般是大于0的数字。 |
| errorMessage | String   | 错误信息，接口调用失败时返回。   |
| 其它     | -        | API 返回的其它数据。                 |

以发起网络请求的 my.request API 为例：

```javascript
// dataType 为 json 示例
my.request({
  url: 'https://httpbin.org/post',
  method: 'POST',
  data: {
    from: '支付宝',
    production: 'AlipayJSAPI',
  },
  dataType: 'json',
  success: function (res) {
    my.alert({ content: 'success' });
  },
  fail: function (res) {
    my.alert({ content: 'fail' });
  },
  complete: function (res) {
    my.alert({ content: 'complete' });
  },
});
```

## 同步型功能 API

以 `Sync` 结尾的 API 都是同步型功能 API，例如 [my.setStorageSync](https://opendocs.alipay.com/mini/api/cog0du)、[my.getBatteryInfoSync](https://opendocs.alipay.com/mini/api/vf7vn3) 等。

同步型功能 API 的执行结果可以通过函数返回值直接获取，如果执行出错会抛出异常：

```javascript
try {
  my.setStorageSync({
    key: 'currentCity',
    data: {
      cityName: '杭州',
      adCode: '330100',
      spell: ' hangzhou',
    },
  });
} catch (e) {
  console.error(e);
}
```

以上为通用说明，特定 API 的入参及返回值以详细 API 文档为准。
