# 简介

**my.ap.getMainSelectedCity** 获取支付宝首页左上角城市的选择信息。

## 使用限制

- 基础库 1.23.7   或更高版本；支付宝客户端  10.1.88  或更高版本，若版本较低，建议做 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 首页优先获取定位城市信息。若用户手动选择过城市，则会替换为用户手动选择的城市。`isManualSelected` 决定是否为手动选择的城市。

# 接口调用

## .axml 示例代码

```html
<view class="page-section">
  <view class="page-section-title">my.ap.getMainSelectedCity</view>
  <view class="page-section-demo">
    <button type="primary" onTap="getMainSelectedCity">
      获取首页选择的城市
    </button>
  </view>
</view>
```

## .js 示例代码

```javascript
Page({
  // getMainSelectedCity
  getMainSelectedCity() {
    if (!my.canIUse('ap.getMainSelectedCity')) {
      my.alert({
        title: '客户端版本过低',
        content: 'getMainSelectedCity 需要 10.1.88 及以上版本',
      });
      return;
    }
    my.ap.getMainSelectedCity({
      success: res => {
        my.alert({
          title: 'getMainSelectedCity response: ' + JSON.stringify(res),
        });
      },
      fail: error => {
        my.alert({
          content: 'getMainSelectedCity error: ' + JSON.stringify(error),
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
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

### Function success

success 回调函数会携带一个 Object 类型的对象，其属性如下：

| **属性**         | **类型** | **描述**                                    |
| ---------------- | -------- | ------------------------------------------- |
| name             | String   | 城市名称。                                  |
| code             | String   | 城市编码。                                  |
| chineseMainLand  | Boolean  | 是否是大陆。                                |
| isManualSelected | Boolean  | 是否是手动选择。                            |
| settingTime      | Number   | 设置时间。                                  |
| districtName     | String   | 区县名（支付宝客户端 10.1.99 版本及以上）。 |
| districtCode     | String   | 区县编码(客户端 10.1.99 版本新增)。         |

## 错误码

| **错误码** | **说明** | **解决方案** |
| --- | --- | --- |
| 10001 | 获取城市信息为空。 | 重新选择城市信息。 |
| 10002 | 城市信息不展示。<br/>支付宝客户端 10.1.90，在支付宝首页的城市选择入口被隐藏时，出现该错误。 | 建议升级支付宝客户端版本。 |
