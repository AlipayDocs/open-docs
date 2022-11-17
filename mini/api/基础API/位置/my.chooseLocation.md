# 简介

**my.chooseLocation** 是使用支付宝内置地图选择地理位置的 API。

## 使用限制

- 暂无境外地图数据，在中国内地以外的地区（不港澳台）使用此 API，功能可能不正常。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验

![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/fbe458f7103f4acf4ca46843964175e5.png#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=stroke&width=127)

## 效果示例

![|300x540](https://gw.alipayobjects.com/zos/skylark-tools/public/files/746fa254e55ffbf7f45a0efb0e0df1e6.gif#align=left&display=inline&height=540&margin=%5Bobject%20Object%5D&originHeight=540&originWidth=300&status=done&style=stroke&width=300)

# 接口调用

## 示例代码

### JavaScript
```javascript
Page({
  data: {
    longitude: '',
    latitude: '',
    name: '',
    address: '',
  },
  chooseLocation() {
    my.chooseLocation({
      success:(res) => {
        console.log(JSON.stringify(res));
        this.setData({
          longitude:res.longitude,
          latitude:res.latitude,
          name:res.name,
          address:res.address
        })
      },
      fail:(error) => {
        my.alert({ content: '调用失败：' + JSON.stringify(error) });
      },
    });
  },
})
```


### AXML
```html
<view class="page">
  <view class="page-section">
    <view class="page-section-demo">
      <text>经度:</text>
      <input value="{{longitude}}"></input>
    </view>
    <view class="page-section-demo">
      <text>纬度:</text>
      <input value="{{latitude}}"></input>
    </view>
    <view class="page-section-demo">
      <text>位置名称:</text>
      <input value="{{name}}"></input>
    </view>
    <view class="page-section-demo">
      <text>详细位置:</text>
      <input value="{{address}}"></input>
    </view>
    <view class="page-section-btns">
      <view onTap="chooseLocation">选择位置</view>
    </view>
  </view>
</view>
```

### ACSS
```css
.page-body-info {
  height: 250rpx;
}
.page-body-text-location {
  display: flex;
  font-size: 50rpx;
}
.page-body-text-location text {
  margin: 10rpx;
}
.page-section-location-text {
  color: #49a9ee;
}
```

## 入参

Object 类型，属性如下：

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| latitude | Number | 否 | 预设纬度，传入该参数将自动定位到该点。 |
| longitude | Number | 否 | 预设经度，传入该参数将自动定位到该点。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

## 出参
success 回调函数携带 Object 类型的参数，包含以下字段：
| **属性** | **类型** | **描述** |
| --- | --- | --- |
| latitude | Number | 纬度，浮点数，范围为-90~90，负数表示南纬 |
| longitude | Number | 经度，浮点数，范围为-180~180，负数表示西经 |
| name | String | 位置名称 |
| provinceName | String | 位置所在省 |
| cityName | String | 位置所在市 |
| address | String | 详细地址 |


## 错误码
fail 回调函数收到 Object 类型的参数，其 errorCode 字段为错误码。
| ** 错误码 ** | **描述** | **解决方案** |
| --- | --- | --- |
| 11 | 用户取消操作 | 无需特殊处理。 |
