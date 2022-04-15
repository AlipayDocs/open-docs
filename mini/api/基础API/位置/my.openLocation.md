
# 简介
**my.openLocation** 是使用支付宝内置地图查看位置的 API。

## 使用限制
- 暂无境外地图数据，在中国内地（不含港澳台）以外的地区可能无法正常调用此 API。
- 仅支持高德地图 style 与火星坐标系。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验
![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/d24dde5bf8bd8b7c34f38dd33b8c589b.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=stroke&width=127)

## 效果示例
![|300x540](https://gw.alipayobjects.com/zos/skylark-tools/public/files/5468fba94664d5e279a2acc5ed365ac6.gif#align=left&display=inline&height=540&margin=%5Bobject%20Object%5D&originHeight=540&originWidth=300&status=done&style=stroke&width=300)

**说明**：点击 **导航** 后，会引导用户打开高德地图；若未安装高德地图，会引导用户下载高德地图。

# 接口调用
## 示例代码
```json
// API-DEMO page/API/open-location/open-location.json
{
    "defaultTitle": "查看位置"
}
```

```html
<!-- API-DEMO page/API/open-location/open-location.axml-->
<view class="page">
  <view class="page-section">
    <view class="page-section-demo">
      <text>经度</text>
      <input type="text" disabled="{{true}}" value="{{longitude}}" name="longitude"></input>
    </view>
    <view class="page-section-demo">
      <text>纬度</text>
      <input type="text" disabled="{{true}}"  value="{{latitude}}" name="latitude"></input>
    </view>
    <view class="page-section-demo">
      <text>位置名称</text>
      <input type="text" disabled="{{true}}"  value="{{name}}" name="name"></input>
    </view>
    <view class="page-section-demo">
      <text>详细位置</text>
      <input type="text" disabled="{{true}}"  value="{{address}}" name="address"></input>
    </view>
    <view class="page-section-btns">
      <view type="primary" formType="submit" onTap="openLocation">查看位置</view>
    </view>
  </view>
</view>
```

```javascript
// API-DEMO page/API/open-location/open-location.js
Page({
  data: {
    longitude: '120.126293',
    latitude: '30.274653',
    name: '黄龙万科中心',
    address: '学院路77号',
  },
  openLocation() {
    my.openLocation({
      longitude: this.data.longitude,
      latitude: this.data.latitude,
      name: this.data.name,
      address: this.data.address,
    })
  }
})
```

## 入参
Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| longitude | String | 是 | 经度。 |
| latitude | String | 是 | 纬度。 |
| name | String | 是 | 位置名称。 |
| address | String | 是 | 地址的详细说明。 |
| scale | Number | 否 | 缩放比例，范围 3 ~ 19，默认为 15。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |
