# 简介
**my.getLocation** 是获取用户当前的地理位置信息的 API。

地图相关接口使用的坐标格式为 [GCJ-02](https://baike.baidu.com/item/GCJ-02)（火星坐标系）。   
暂无境外地图数据，在中国内地（不含港澳台）以外的地区可能无法正常调用此 API。   

## 使用限制

- 此 API 实际表现请以真机为准。
- 基础库 [1.1.1](https://opendocs.alipay.com/mini/framework/lib) 或更高版本开始支持。若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验

![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/1f4398769e1318eb107ea8e54f03f2f8.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=stroke&width=127)

## 效果示例

![|300x540](https://gw.alipayobjects.com/zos/skylark-tools/public/files/da3503152827b4db465e75483664b260.gif#align=left&display=inline&height=540&margin=%5Bobject%20Object%5D&originHeight=540&originWidth=300&status=done&style=stroke&width=300)

# 接口调用

## 示例代码

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

format-location.js 示例代码如下：

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
页面 .js 示例代码如下：
```javascript
// API-DEMO page/API/get-location/get-location.js
import formatLocation from './format-location.js';
Page({
  data: {
    hasLocation: false,
  },
  getLocation() {
    my.showLoading();
    my.getLocation({
      success: (res) => {
        my.hideLoading();
        console.log(res);
        this.setData({
          hasLocation: true,
          location: formatLocation(res.longitude, res.latitude)
        })
      },
      fail: (res) => {
        my.hideLoading();
        console.log(res.error, res.errorMessage);
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

## 入参

Object 类型，属性如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| cacheTimeout | Number | 否 | 支付宝客户端经纬度定位缓存过期时间，单位为秒。默认 30 秒（s）。 <br>使用缓存会加快定位速度，缓存过期会重新定位。 |
| type | Number | 否 | 获取经纬度数据的类型。默认值为 0。<ul><li>0：获取经纬度。</li><li>1：获取经纬度和详细到区县级别的[逆地理编码](https://baike.baidu.com/item/%E9%80%86%E5%9C%B0%E7%90%86%E4%BF%A1%E6%81%AF)数据。</li><li>2：获取经纬度和详细到街道级别的逆地理编码数据，不推荐使用。（不推荐使用的原因：精度过高，接口返回的速度会变慢。）</li><li>3：获取经纬度和详细到POI级别的逆地理编码数据，不推荐使用。（不推荐使用的原因：精度过高，接口返回的速度会变慢。）</li></ul> |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

### success 回调函数

success 回调函数会携带一个 Object 类型的对象，其属性如下：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| longitude | String | 经度 |
| latitude | String | 纬度 |
| accuracy | String | 精确度，单位米 (m)。 |
| horizontalAccuracy | String | 水平精确度，单位为米 (m)。 |
| country | String | 国家（type > 0 生效）。 |
| countryCode | String | 国家编号 （type>0生效）。|
| province | String | 省份（type > 0生效）。|
| provinceAdCode | String | 省份级别的地区代码（type > 0 生效）。|
| city | String | 城市（type > 0 生效）。|
| cityAdcode | String | 城市级别的地区代码（type>0 生效）。 |
| district | String | 区县（type > 0 生效）。 |
| districtAdcode | String | 区县级别的地区代码（type > 0 生效）。 |
| streetNumber | Object | 需要街道级别逆地理的才会有的字段,街道门牌信息，结构是：`{street, number}`（type > 1 生效）。 |
| pois | Array | 需要 POI （Point of Interest，兴趣点，在地理信息系统中，一个 POI 可以是一栋房子、一个商铺、一个邮筒、一个公交站等）级别的地理位置才会有的字段，定位点附近的 POI 信息，结构是：{name, address}（type > 2 生效）。 |

### fail 回调函数

fail 回调函数会携带一个 Object 类型的对象，其属性如下：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| error | Number | 错误码。 |
| errorMessage | String | 错误信息。 |

## 错误码
| **错误码** | **描述** | **解决方案** |
| --- | --- | --- |
| 11 | 请确认定位相关权限已开启。包含 “GPS未开启” 和 “未打开允许支付宝使用定位的开关” 两种情况。 | 提示用户打开 GPS 或者 确认是否已给支付宝客户端获取定位权限。 |
| 12 | 网络异常，请稍后再试。 | 提示用户检查当前网络。 |
| 13 | 定位失败，请稍后再试。 | 提示用户再次尝试。 |
| 14 | 业务定位超时。 | 提示用户再次尝试。 |
| 2001 | 用户拒绝给小程序授权。 | 提示用户接受小程序授权。 |

# 常见问题

## Q：my.getLocation 第一次允许授权后删除小程序应用，重新打开会需要重新授权吗？ 

A：需要重新授权，删除小程序应用后会将获取定位的授权关系一起删除。

## Q：小程序如何区分 “未授权位置信息给支付宝APP” 和 “GPS未开启” 两种状态。

A：错误码为 11 时， 包含 “GPS未开启” 和 “未打开允许支付宝使用定位的开关” 两种情况。此时，可通过 my.getSystemSetting 接口的返回参数 locationEnabled 来判断用户是否开启地理位置的系统开关。

