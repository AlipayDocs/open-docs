# 简介
**my.getLocation** 是获取用户当前的地理位置信息的 API。

地图相关接口使用的坐标格式为 GCJ-02（火星坐标系）。   
暂无境外地图数据，在中国内地（不含港澳台）以外的地区可能无法正常调用此 API。   

## 使用限制

- 基础库 [1.1.1](https://opendocs.alipay.com/mini/framework/lib) 或更高版本开始支持。若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验

![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/1f4398769e1318eb107ea8e54f03f2f8.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=stroke&width=127)

## 效果示例

![|300x540](https://gw.alipayobjects.com/zos/skylark-tools/public/files/da3503152827b4db465e75483664b260.gif#align=left&display=inline&height=540&margin=%5Bobject%20Object%5D&originHeight=540&originWidth=300&status=done&style=stroke&width=300)

# 接口调用

## 示例代码

### .axml 示例代码

```html
<!-- get-location.axml-->
<view class="page">
  <view class="page-section">
    <view class="page-section-btns">
        <button onTap="getLocation">获取位置</button>
    </view>
    <view class="page-section-demo">
      <block a:if="{{hasLocation === true}}">
        <view>当前位置经纬度</view>
        <view class="page-body-text-location">
          <view>经度: {{longitude}}</view>
          <view>纬度: {{latitude}}</view>
        </view>
      </block>
    </view>
  </view>
</view>
```

### .js 示例代码
```javascript
// get-location.js
Page({
  data: {
    hasLocation: false,
    longitude: 0,
    latitude: 0,
  },
  getLocation() {
    my.showLoading();
    my.getLocation({
      type: 1, //获取区县数据
      success: (res) => {
        console.log(res);
        this.setData({
          hasLocation: true,
          longitude: res.longitude,
          latitude: res.latitude
        })
      },
      fail: (res) => {
        my.alert({ title: '定位失败' });
      },
      complete: () => {
        my.hideLoading();
      },
    })
  }
})
```

## 入参

Object 类型，属性如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| cacheTimeout | Number | 否 | 支付宝客户端经纬度定位缓存过期时间，单位为秒。默认 30 秒（s）。 <br>使用缓存会加快定位速度，缓存过期会重新定位。 |
| type | Number | 否 | 获取经纬度数据的类型。默认值为 0。<ul><li>0：获取经纬度。</li><li>1：获取经纬度和区县数据。</li><li>2：获取经纬度、区县和街道数据，不推荐使用。（不推荐使用的原因：精度过高，接口返回的速度会变慢。）</li><li>3：获取经纬度、区县、街道和详细到 POI 级别的数据，不推荐使用。不推荐使用的原因：精度过高，接口返回的速度会变慢。</li></ul> |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

### success 回调函数

success 回调函数会携带一个 Object 类型的对象，其属性如下：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| longitude | String | 经度，范围为 -180~180，负数表示西经 |
| latitude | String | 纬度，范围为 -90~90，负数表示南纬 |
| accuracy | String | 精确度，单位米 (m)。 |
| horizontalAccuracy | String | 水平精确度，单位为米 (m)。 |
| country | String | 国家（type > 0 生效）。 |
| countryCode | String | 国家编号 （type>0生效）。|
| province | String | 省份（type > 0生效）。|
| provinceAdcode | String | 省份级别的地区代码（type > 0 生效）。|
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
| 11 | 请确认定位相关权限已开启。 | 包含 “GPS未开启” 和 “未打开允许支付宝使用定位的开关” 两种情况。参照 常见问题 Q1 |
| 12 | 网络异常，请稍后再试。 | 提示用户检查当前网络。 |
| 13 | 定位失败，请稍后再试。 | 提示用户再次尝试。 |
| 14 | 业务定位超时。 | 提示用户再次尝试。 |
| 18 | 获取到的基站与WIFI为空，请您打开WIFI开关，如已打开，建议移动到有WIFI的区域在发起定位 | 提示用户确认WIFI开关是否打开。如已打开，提示用户移动到有WIFI的区域再发起定位。 |
| 2001 | 用户拒绝给小程序授权。 | 提示用户接受小程序授权。 |
| 2002 | 保持拒绝后再触发定位。 | 小程序右上角点击更多 "..." -> 设置 -> 地理位置关闭，可以更改保持状态。 |
| 2003 | 勾选保持后再点选了拒绝。 | 小程序右上角点击更多 "..." -> 设置 -> 地理位置关闭，可以更改保持状态。 |

# 常见问题 FAQ

## Q：如果系统权限未开启，接口调用报错，如何引导开启系统权限？
A：可以调用 [my.showAuthGuide](https://opendocs.alipay.com/mini/api/show-auth-guide) 引导用户开启相关系统权限。

## Q：my.getLocation 第一次允许授权后删除小程序应用，重新打开会需要重新授权吗？ 
A：需要重新授权，删除小程序应用后会将获取定位的授权关系一起删除。

## Q：如何在 IDE 模拟器调试 my.getLocation 接口？
A：可以在模拟器工具栏中点击定位按钮，自定义当前位置的经纬度。<br />![](https://img.alicdn.com/imgextra/i1/O1CN01jQG0oE1ZOJqojXjqo_!!6000000003184-0-tps-456-266.jpg)


## Q：my.getLocation 在 IDE 模拟器中获取的地理位置信息不对？
A：IDE 模拟器目前默认的地址是杭州，后期会优化。如果想要在 IDE 模拟器中调试 my.getLocation 接口，请参考 “如何在 IDE 模拟器调试 my.getLocation 接口？” FAQ。

## Q：my.getLocation 怎么获取省市区？
A：type 入参为1、2、3都可以获取到省市区及其相对应的行政区划编码。不推荐使用2、3，使用2、3精度过高，接口返回的速度会变慢。
```javascript
my.getLocation({
  type: 1,
  success: (res) => {
    console.log(res);
  },
  fail: (res) => {
    console.log(res);
    my.alert({ title: '定位失败' });
  },
  complete: (res) => {
  
  },
})
```

## Q：my.getLocation 报错 code 2003 、 2002 和 2001 的区别？
A：
| **错误码** | **描述** |
| --- | --- |
| 2003 | 当触发位置授权弹窗提示时，用户勾选了 “总是保持以上选择，不再询问”，然后再点击拒绝时就会报错2003。 |
| 2002 | 当用户之前已经勾选过 “总是保持以上选择，不再询问”，用户再次触发 my.getLocation API时会报错2002。 |
| 2001 | 当触发位置授权弹窗提示时，不勾选 “总是保持以上选择，不再询问”，直接拒绝就会报错2001。 |

## Q：my.getLocation 怎么再次唤起位置授权弹窗？
A：
- 使用 my.openSetting 打开小程序设置界面，地理位置选择关闭，再次触发 my.getLocation 方法就会唤起授权弹窗。
- 或者小程序右上角点击更多 "..." -> 设置 -> 地理位置，选择“关闭”，再次触发 my.getLocation 方法也会唤起授权弹窗。
