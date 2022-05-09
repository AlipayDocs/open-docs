
# 简介
**my.getNetworkType** 是获取当前网络状态的 API。

## 使用限制
此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验
![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/22ff3ede2bb9a8def0ff2814a28690d2.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=none&width=127)

# 接口调用

## 示例
[小程序在线](https://opendocs.alipay.com/examples/98a14a36-e111-4292-96ee-3ef9122ca63a) 

### .json 示例代码
```json
// API-DEMO page/API/get-network-type/get-network-type.json
{
    "defaultTitle": "获取手机网络状态"
}
```

### .axml 示例代码
```html
<!-- API-DEMO page/API/get-network-type/get-network-type.axml-->
<view class="page">
  <view class="page-section">
    <view class="page-section-demo">
      <view class="page-body-title">网络状态</view>
      <block a:if="{{hasNetworkType === false}}">
        <text class="page-body-text">未获取</text>
        <text class="page-body-text">点击按钮可获取网络状态</text>
      </block>
      <block a:if="{{hasNetworkType === true}}">
        <text class="page-body-text-network-type">{{networkType}}</text>
      </block>
    </view>
    <view class="page-section-btns">
      <view onTap="getNetworkType">获取手机网络状态</view>
      <view onTap="clear">清空</view>
    </view>
  </view>
</view>
```

### .js 示例代码

```javascript
// API-DEMO page/API/get-network-type/get-network-type.js
Page({
  data: {
    hasNetworkType: false
  },
  onLoad() {
    this.onChange = this.onChange.bind(this);
    // my.onNetworkChange(this.onChange);
  },
  onChange(res){
    console.log('onNetworkChange', res);
    this.setData({
      hasNetworkType: true,
      networkType: res.networkType
    });
  },
  onUnload() {
    // my.offNetworkChange(this.onChange);
  },
  getNetworkType() {
    my.getNetworkType({
      success: (res) => {
        this.setData({
          hasNetworkType: true,
          networkType: res.networkType
        })
      }
    })
  },
  clear() {
    this.setData({
      hasNetworkType: false,
      networkType: ''
    })
  },
});
```

### .acss 示例代码

```
/* API-DEMO page/API/get-network-type/get-network-type.acss */
.page-body-info {
  height: 200rpx;
}
.page-body-text-network-type {
  font-size: 80rpx;
  font-family: Helvetica;
}
```

## 入参
Object 类型，属性如下：

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |


### success 回调函数
入参为 Object 类型，属性如下：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| networkAvailable | Boolean | 网络是否可用。 |
| networkType | String | 网络类型值 UNKNOWN / NOTREACHABLE / WIFI / 3G / 2G / 4G / WWAN。 |

