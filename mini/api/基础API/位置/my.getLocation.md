
# 简介
**my.getLocation** 是获取用户当前的地理位置信息的 API。

## 使用限制

- 基础库 [1.1.1](https://opendocs.alipay.com/mini/framework/lib) 或更高版本。若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 暂无境外地图数据，在中国内地（不含港澳台）以外的地区可能无法正常调用此 API。
- 仅支持高德地图 style 与火星坐标系（GCJ-02）。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验
![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/1f4398769e1318eb107ea8e54f03f2f8.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=stroke&width=127)

## 效果示例
![|300x540](https://gw.alipayobjects.com/zos/skylark-tools/public/files/da3503152827b4db465e75483664b260.gif#align=left&display=inline&height=540&margin=%5Bobject%20Object%5D&originHeight=540&originWidth=300&status=done&style=stroke&width=300)


# 接口调用

## 示例代码

### .json 示例代码
```json
// API-DEMO page/API/get-location/get-location.json
{
    "defaultTitle": "获取位置"
}
```

### .axml 示例代码
```html
<!-- API-DEMO page/API/get-location/get-location.axml-->
<view class="page">
  <view class="page-section">
    <view class="page-section-demo">
      <view>当前位置经纬度</view>
      <block a:if="{{hasLocation === false}}">
        <text>未获取</text>
      </block>
      <block a:if="{{hasLocation === true}}">
        <view class="page-body-text-location">
          <text>E{{location.longitude[0]}}°{{location.longitude[1]}}′</text>
          <text>N{{location.latitude[0]}}°{{location.latitude[1]}}′</text>
        </view>
      </block>
    </view>
    <view class="page-section-btns">
      <view onTap="getLocation">获取位置</view>
      <view onTap="clear">清空</view>
    </view>
  </view>
</view>
```

### .js 示例代码
```javascript
// API-DEMO page/API/get-location/format-location.js
function formatLocation(longitude, latitude) {
  longitude = Number(longitude).toFixed(2),
  latitude = Number(latitude).toFixed(2)
  return {
    longitude: longitude.toString().split('.'),
    latitude: latitude.toString().split('.')
  }
}
export default formatLocation
```

### .js 示例代码
```javascript
// API-DEMO page/API/get-location/get-location.js
import formatLocation from './format-location.js';
Page({
  data: {
    hasLocation: false,
  },
  getLocation() {
    var that = this;
    my.showLoading();
    my.getLocation({
      success(res) {
        my.hideLoading();
        console.log(res)
        that.setData({
          hasLocation: true,
          location: formatLocation(res.longitude, res.latitude)
        })
      },
      fail() {
        my.hideLoading();
        my.alert({ title: '定位失败' });
      },
    })
  },
  clear() {
    this.setData({
      hasLocation: false
    })
  }
})
```

### .acss 示例代码
```css
/* API-DEMO page/API/get-location/get-location.acss */
.page-body-info {
  height: 250rpx;
}
.page-body-text-small {
  font-size: 24rpx;
  color: #000;
  margin-bottom: 100rpx;
}
.page-body-text-location {
  display: flex;
  font-size: 50rpx;
}
.page-body-text-location text {
  margin: 10rpx;
}
```

## 入参
Object 类型，属性如下：

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| cacheTimeout | Number | 否 | 支付宝客户端经纬度定位缓存过期时间，单位为秒。默认 30 秒（s）。使用缓存会加快定位速度，缓存过期会重新定位。 |
| type | Number | 否 | 获取经纬度数据的类型。默认值为 0。最低基础库版本限制为 [1.1.1](https://opendocs.alipay.com/mini/framework/lib)。<li>0：获取经纬度。</li><li>1：获取经纬度和详细到区县级别的逆地理编码数据。</li><li>2：获取经纬度和详细到街道级别的逆地理编码数据，不推荐使用。（不推荐使用的原因：精度过高，接口返回的速度会变慢。）</li><li>3：获取经纬度和详细到POI级别的逆地理编码数据，不推荐使用。（不推荐使用的原因：精度过高，接口返回的速度会变慢。）</li>|
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |


### success 回调函数
| **属性** | **类型** | **描述** |
| --- | --- | --- |
| longitude | String | 经度 |
| latitude | String | 纬度 |
| accuracy | String | 精确度，单位米 (m)。 |
| horizontalAccuracy | String | 水平精确度，单位为米 (m)。 |
| country | String | 国家（type>0生效）。<br />最低基础库版本限制为 [1.1.1](https://opendocs.alipay.com/mini/framework/lib)。 |
| countryCode | String | 国家编号 （type>0生效）。<br />最低基础库版本限制为 [1.1.1](https://opendocs.alipay.com/mini/framework/lib)。 |
| province | String | 省份（type>0生效）。<br />最低基础库版本限制为 [1.1.1](https://opendocs.alipay.com/mini/framework/lib)。 |
| provinceAdCode | String | 省份级别的地区代码（type>0生效）。<br />最低基础库版本限制为 [1.1.1](https://opendocs.alipay.com/mini/framework/lib)。 |
| city | String | 城市（type>0生效）。<br />最低基础库版本限制为 [1.1.1](https://opendocs.alipay.com/mini/framework/lib)。 |
| cityAdcode | String | 城市级别的地区代码（type>0生效）。<br />最低基础库版本限制为 [1.1.1](https://opendocs.alipay.com/mini/framework/lib)。 |
| district | String | 区县（type>0生效）。<br />最低基础库版本限制为 [1.1.1](https://opendocs.alipay.com/mini/framework/lib)。 |
| districtAdcode | String | 区县级别的地区代码（type>0生效）。<br />最低基础库版本限制为 [1.1.1](https://opendocs.alipay.com/mini/framework/lib)。 |
| streetNumber | Object | 需要街道级别逆地理的才会有的字段,街道门牌信息，结构是：{street, number} （type>1生效）。<br />最低基础库版本限制为 [1.1.1](https://opendocs.alipay.com/mini/framework/lib)。 |
| pois | Array | 需要 POI （Point of Interest，兴趣点，在地理信息系统中，一个 POI 可以是一栋房子、一个商铺、一个邮筒、一个公交站等）级别的地理位置才会有的字段，定位点附近的 POI 信息，结构是：{name, address}（type>2生效）。<br />最低基础库版本限制为 [1.1.1](https://opendocs.alipay.com/mini/framework/lib)。 |


### fail 回调函数
Object 类型，属性如下：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| error | String | 错误码。 |
| errorMessage | String | 错误信息。 |


## 错误码
| **错误码** | **描述** | **解决方案** |
| --- | --- | --- |
| 11 | 请确认定位相关权限已开启。 | 提示用户确认手机是否已给支付宝 APP 获取定位权限。 |
| 12 | 网络异常，请稍后再试。 | 提示用户检查当前网络。 |
| 13 | 定位失败，请稍后再试。 | 提示用户再次尝试。 |
| 14 | 业务定位超时。 | 提示用户再次尝试。 |
| 2001 | 用户拒绝给小程序授权。 | 提示用户接受小程序授权。 |


## 常见问题 FAQ

### Q：my.getLocation 第一次允许授权后删除小程序应用，重新打开会需要重新授权吗？ 

A：需要重新授权，删除小程序应用后会将获取定位的授权关系一起删除。
