# 简介
**my.datePicker** 是打开日期选择列表的 API。

## 使用限制

此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验

![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/8652e218e6d945058e66d1fd2eafc101.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=none&width=127)

# 接口调用

## 示例
[小程序在线](https://opendocs.alipay.com/examples/eccf6b98-6a66-4584-8c36-2020d618b6a9) 

### .json 示例代码

```json
{
    "defaultTitle": "Date Picker"
}
```

### .axml 示例代码

```html
<!-- API-DEMO page/API/date-picker/date-picker.axml -->
<view class="page">
  <view class="page-description">选择日期 API</view>
  <view class="page-section">
    <view class="page-section-title">my.datePicker</view>
    <view class="page-section-demo">
      <button class="page-body-button" type="primary" onTap="datePicker">选择日期-1</button>
      <button class="page-body-button" type="primary" onTap="datePickerHMS">选择日期-2</button>
      <button class="page-body-button" type="primary" onTap="datePickerYMDHMS">选择日期-3</button>
    </view>
  </view>
</view>
```

### .js 示例代码

```javascript
// API-DEMO page/API/date-picker/date-picker.js
Page({
  datePicker() {
    my.datePicker({
      currentDate: '2016-10-10',
      startDate: '2016-10-9',
      endDate: '2017-10-9',
      success: (res) => {
        my.alert({
          title: 'datePicker response: ' + JSON.stringify(res)
        });
      },
    });
  },
  datePickerHMS() {
    my.datePicker({
      format: 'HH:mm',
      currentDate: '12:12',
      startDate: '11:11',
      endDate: '13:13',
      success: (res) => {
        my.alert({
          title: 'datePicker response: ' + JSON.stringify(res)
        });
      },
    });
  },
  datePickerYMDHMS() {
    my.datePicker({
      format: 'yyyy-MM-dd HH:mm',
      currentDate: '2012-01-09 11:11',
      startDate: '2012-01-01 11:11',
      endDate: '2012-01-10 11:11',
      success: (res) => {
        my.alert({
          title: 'datePicker response: ' + JSON.stringify(res)
        });
      },
    });
  },
});
```

### .acss 示例代码

```css
/* API-DEMO page/API/date-picker/date-picker.acss */
button + button {
  margin-top: 20rpx;
}
```

## 入参

Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| format | String | 否 | 返回的日期格式。<br /><ul><li>yyyy-MM-dd（默认）。</li><li>HH:mm 。</li><li>yyyy-MM-dd HH:mm 。</li><li>yyyy-MM（最低基础库版本：[1.1.1](https://opendocs.alipay.com/framework/compatibility)，可通过 `canIUse('datePicker.object.format.yyyy-MM')` 判断）。</li><li>yyyy（最低基础库版本：<b>1.1.1</b>，可通过 `canIUse('datePicker.object.format.yyyy')` 判断）。</li></ul> |
| currentDate | String | 否 | 初始选择的日期时间，默认当前时间。 |
| startDate | String | 否 | 最小日期时间。 |
| endDate | String | 否 | 最大日期时间。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |


### Function success

success 回调函数会携带一个 Object 类型的对象，其属性如下：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| date | String | 选择的日期。 |


## 错误码
| **错误码** | **描述** | **解决方案** |
| --- | --- | --- |
| 11 | 用户取消操作。 | 这是用户正常交互流程分支，不需要特殊处理。 |

