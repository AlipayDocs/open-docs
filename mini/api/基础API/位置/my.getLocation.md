# 简介

**my.getLocation** 是获取用户当前的地理位置信息的 API。

地图相关接口使用的坐标格式为 GCJ-02（火星坐标系）。  
暂无境外地图数据，在中国内地（不含港澳台）以外的地区可能无法正常调用此 API。
<br />获取到定位的前提，是有定位权限，定位权限包含系统位置权限、支付宝定位权限以及小程序位置权限，缺少任何一种定位权限都无法定位。更多信息可查看[小程序定位权限原理](https://opendocs.alipay.com/mini/api/mkxuqd#Q：小程序定位授权的原理是什么？)

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
      type: 1, //获取经纬度和省市区县数据
      success: (res) => {
        console.log(res);
        this.setData({
          hasLocation: true,
          longitude: res.longitude,
          latitude: res.latitude,
        });
      },
      fail: (res) => {
        my.alert({ title: '定位失败', content: JSON.stringify(res) });
      },
      complete: () => {
        my.hideLoading();
      },
    });
  },
});
```

## 入参

Object 类型，属性如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| cacheTimeout | Number | 否 | 支付宝客户端经纬度定位缓存过期时间，单位为秒。默认 30 秒（s）。<br>使用缓存会加快定位速度，缓存过期会重新定位。 |
| type | Number | 否 | 获取经纬度数据的类型。默认值为 0。<ul><li>0：获取经纬度。</li><li>1：获取经纬度和省市区县数据。</li><li>2：获取经纬度、省市区县和街道数据，通常不推荐使用（原因：精度过高，接口返回的速度会变慢）。</li><li>3：获取经纬度、省市区县、街道和详细到 POI 级别的数据，通常不推荐使用（原因：精度过高，接口返回的速度会变慢）。</li></ul> |
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
| countryCode | String | 国家编号 （type>0 生效）。 |
| province | String | 省份（type > 0 生效）。 |
| provinceAdcode | String | 省份级别的地区代码（type > 0 生效）。 |
| city | String | 城市（type > 0 生效）。 |
| cityAdcode | String | 城市级别的地区代码（type>0 生效）。 |
| district | String | 区县（type > 0 生效）。 |
| districtAdcode | String | 区县级别的地区代码（type > 0 生效）。 |
| streetNumber | Object | 需要街道级别逆地理的才会有的字段,街道门牌信息，结构是：`{street, number}`（type > 1 生效）。 |
| pois | Array | 需要 POI （Point of Interest，兴趣点，在地理信息系统中，一个 POI 可以是一栋房子、一个商铺、一个邮筒、一个公交站等）级别的地理位置才会有的字段，定位点附近的 POI 信息，结构是：{name, address}（type > 2 生效）。 |

### fail 回调函数

fail 回调函数会携带一个 Object 类型的对象，其属性如下：

| **属性**     | **类型** | **描述**   |
| ------------ | -------- | ---------- |
| error        | Number   | 错误码。   |
| errorMessage | String   | 错误信息。 |

## 错误码

| **错误码** | **报错信息** | **描述** | **解决方案** |
| --- | --- | --- | --- |
| 11 | 请确认定位相关权限已开启 | 包含用户未授权系统位置权限和支付宝定位权限两种情况。 | 接入定位权限引导，引导用户开启定位权限。参考开放平台 [my.showAuthGuide](https://opendocs.alipay.com/mini/api/show-auth-guide) 文档。 |
| 12 | 网络异常，请稍后再试。 || 提示用户检查当前网络。 |
| 13 | 定位失败，请稍后再试。 || 提示用户再次尝试。 |
| 14 | 业务定位超时。 || 提示用户再次尝试。 |
| 18 | 获取到的基站与 WIFI 为空，请您打开 WIFI 开关，如已打开，建议移动到有 WIFI 的区域在发起定位 || 提示用户确认 WIFI 开关是否打开。如已打开，提示用户移动到有 WIFI 的区域再发起定位。 |
| 2001 | 用户不允许授权 | 当用户授权系统位置权限和支付宝定位权限两种情况后，用户触发位置授权弹窗提示时不勾选 “总是保持以上选择，不再询问”，直接拒绝就会报错2001。 | 提示用户接受小程序授权并再次触发 my.getLocation API。 |
| 2002 | 用户不允许授权 | 当用户授权系统位置权限和支付宝定位权限两种情况后，用户之前已经勾选了 “总是保持以上选择，不再询问”，当用户再次触发 my.getLocation API时会就报错2002，并且不会弹出授权弹窗。 | 即为永久拒绝，使用 [my.openSetting](https://opendocs.alipay.com/mini/api/qflu8f) 打开小程序设置界面，选择地理位置，再次触发 my.getLocation API即可。 |
| 2003 | 用户勾选了不允许授权选项 |当用户授权系统位置权限和支付宝定位权限两种情况后，用户触发位置授权弹窗并勾选了 “总是保持以上选择，不再询问”，然后再点击拒绝时就会报错2003。 | 即为永久拒绝，使用 [my.openSetting](https://opendocs.alipay.com/mini/api/qflu8f) 打开小程序设置界面，选择地理位置，再次触发 my.getLocation API即可。 |

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
    my.alert({ title: '定位失败', content: JSON.stringify(res) });
  },
})
```

## Q：my.getLocation 永久拒绝获取定位权限之后，怎么再次唤起位置授权弹窗？
A：

**什么是永久拒绝？**
<br />当触发位置授权弹窗提示时，用户勾选 “总是保持以上选择，不再询问”，然后再点击拒绝，即为永久拒绝。<br /><img src="https://img.alicdn.com/imgextra/i4/O1CN01EPmlU01vsTTYYJK6v_!!6000000006228-0-tps-820-888.jpg" width="250px">

**永久拒绝后怎么再次唤起位置授权弹窗？**
- 使用 my.openSetting 打开小程序设置界面，地理位置，再次触发 my.getLocation 方法就会唤起授权弹窗。
- 或者小程序右上角点击更多 "..." -> 设置 -> 地理位置，再次触发 my.getLocation 方法也会唤起授权弹窗。

## Q：怎么查看小程序区域编码？
A：点击[链接](https://opendocs.alipay.com/isv/10327/yqo8m9)下载查看。

## Q：小程序定位授权的原理是什么？
A：
获取到定位的前提，是有定位权限，如下图所示，定位权限包含系统位置权限、支付宝定位权限以及小程序位置权限，缺少任何一种定位权限都无法定位。<br /><img src="https://img.alicdn.com/imgextra/i2/O1CN01dem1e81lgtIkL1ggP_!!6000000004849-2-tps-304-157.png" width="250px">

**系统位置权限**
<br />用户需要打开手机系统定位权限

- ios图示 <br /><img src="https://img.alicdn.com/imgextra/i4/O1CN01e2Kj7J23ZFmNq6f4H_!!6000000007269-2-tps-398-437.png" width="250px">

- 安卓图示 <br /><img src="https://img.alicdn.com/imgextra/i4/O1CN01e2Kj7J23ZFmNq6f4H_!!6000000007269-2-tps-398-437.png" width="250px">

**支付宝定位权限**
<br />打开系统位置权限后，需要授予支付宝定位权限

- ios图示 <br /><img src="https://img.alicdn.com/imgextra/i4/O1CN01L2bsQw1gcFCf40Rvd_!!6000000004162-2-tps-398-471.png" width="250px">

- 安卓图示 <br /><img src="https://img.alicdn.com/imgextra/i2/O1CN01UGE8KL22CWVesTWKV_!!6000000007084-2-tps-755-1081.png" width="250px">

**小程序定位权限**
<br />打开系统定位权限并授予支付宝定位权限后，需要用户授予小程序定位权限
<br /><img src="https://img.alicdn.com/imgextra/i2/O1CN01UGE8KL22CWVesTWKV_!!6000000007084-2-tps-755-1081.png" width="250px">
