# 简介

**my.getLocation** 获取用户所处地理位置。可获取经纬度（坐标格式为 GCJ-02），也可通过指定适当的入参获取省市区县乃至街道地址。

## 定位授权

调用 my.getLocation 接口获取用户地理位置信息，需要有用户授权，包含三层：
1，系统开启了定位功能；
2，系统已对支付宝授权位置信息；
3，用户在 my.getLocation 调用时弹出的位置信息授权框里选择同意授权给当前小程序。

这三条必须全部满足，否则将触发 fail 回调：不满足 1 或 2，fail 回调错误码为 11；不满足 3，fail 回调错码误为 2001/2002/2003。

## 出错处理

除用户授权以外，地理位置的成功获取也依赖用户手机当前的状态，如有 GPS 或基站信号、有正常的网络连接等。各种出错的可能及处理措施，请参考后文**错误码**表格中的解决方案。


## 使用限制

- 基础库 [1.1.1](https://opendocs.alipay.com/mini/framework/lib) 或更高版本开始支持。若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。
- 无境外地图数据，在中国内地（不含港澳台）以外的地区使用此 API 可能无法得到预期结果。


## 扫码体验

![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/1f4398769e1318eb107ea8e54f03f2f8.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=stroke&width=127)


## 效果示例

![|300x540](https://gw.alipayobjects.com/zos/skylark-tools/public/files/da3503152827b4db465e75483664b260.gif#align=left&display=inline&height=540&margin=%5Bobject%20Object%5D&originHeight=540&originWidth=300&status=done&style=stroke&width=300)


# 接口调用

## 示例代码

### .js 示例代码

```javascript
Page({
  data: {
    hasLocation: false,
    longitude: 0,
    latitude: 0,
  },
  getLocation() {
    my.showLoading();
    my.getLocation({
      type: 1, // 获取经纬度和省市区县数据
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

### .axml 示例代码

```html
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

## 入参

Object 类型，属性如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| type | Number | 否 | 获取经纬度数据的类型。默认值为 0。<ul><li>0：获取经纬度。</li><li>1：获取经纬度和省市区县数据。</li><li>2：获取经纬度、省市区县和街道数据，通常不推荐使用（速度慢）。</li><li>3：获取经纬度、省市区县、街道和周边 POI 数据，通常不推荐使用（速度更慢）。</li></ul> |
| cacheTimeout | Number | 否 | 缓存过期时间，单位为秒。默认 30 秒（s）。 <br>未过期的缓存数据会直接返回（速度快），缓存过期会重新定位（速度慢）。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

### success 回调函数

success 回调函数会携带一个 Object 类型的对象，默认（入参 type 为 0 时）属性如下：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| longitude | String | 经度，范围为 -180~180，负数表示西经。 |
| latitude | String | 纬度，范围为 -90~90，负数表示南纬。 |
| accuracy | String | 精确度，单位米 (m)。 |
| horizontalAccuracy | String | 水平精确度，单位为米 (m)。 |

当入参 type 为 1 或者 2 时，success 的参数会带有如下额外属性：
| **属性** | **类型** | **描述** |
| --- | --- | --- |
| country | String | 国家。 |
| countryCode | String | 国家编号。 |
| province | String | 省份。 |
| provinceAdcode | String | 省份的地区代码。 |
| city | String | 城市。 |
| cityAdcode | String | 城市的地区代码。 |
| district | String | 区县。 |
| districtAdcode | String | 区县的地区代码。 |

当入参 type 为 2 时，success 的参数会带有如下额外属性：
| **属性** | **类型** | **描述** |
| --- | --- | --- |
| streetNumber | Object | 街道门牌信息，结构是：`{street, number}`（入参 type > 1 生效）。 |
| pois | Array<Object> | 定位点附近的 POI（兴趣点） 列表（type > 2 生效）。<br>POI 的结构是 `{name, address}`，表示一个地图上有意义的点，可能是一栋建筑、一个商铺、一个邮筒、一个公交站等。 |


### fail 回调函数

fail 回调函数会携带一个 Object 类型的对象，包含如下属性：

| **属性**     | **类型** | **描述**   |
| ------------ | -------- | ---------- |
| error        | Number   | 错误码。   |
| errorMessage | String   | 错误信息。 |


## 错误码

| **错误码** | **报错信息** | **说明** | **解决方案** |
| --- | --- | --- | --- |
| 11 | 请确认定位相关权限已开启 | 用户设备未开启定位功能，或未授予支付宝定位权限（如有必要可通过 my.getSystemInfo 区分具体是哪一种情况）。 | 调用 [my.showAuthGuide](https://opendocs.alipay.com/mini/api/show-auth-guide) 以引导用户开启定位并授权给支付宝。 |
| 12 | 网络异常，请稍后再试。 || 提示用户检查网络。 |
| 13 | 定位失败，请稍后再试。 || 提示用户再次尝试。 |
| 14 | 业务定位超时。 | 定位超过内部时限未能返回结果。 | 提示用户再次尝试。 |
| 18 | 获取到的基站与 WIFI 为空，请您打开 WIFI 开关，如已打开，建议移动到有 WIFI 的区域再发起定位。 || 提示用户在有手机信号或有 WiFi 的区域再次尝试，且确保打开 WiFi 开关。 |
| 2001 | 用户不允许授权。 | 用户在对小程序授权地理位置的提示弹框里点击了拒绝。 | 向用户说明小程序获取地理位置的必要性，然后再次调用 my.getLocation。 |
| 2003 | 用户勾选了不允许授权选项。 | 用户在对小程序授权地理位置的提示弹框里点击了拒绝，且同时勾选了 “总是保持以上选择，不再询问”。 | 向用户说明获取地理位置的必要性，调用 my.openSetting 帮用户打开小程序设置界面。|
| 2002 | 用户不允许授权。 | 用户之前已经拒绝授权且勾选了“总是保持以上选择，不再询问”，本次调用 my.getLocation 直接失败，不会弹出授权提示。 | 向用户说明获取地理位置的必要性，调用 my.openSetting 帮用户打开小程序设置界面。|
| 其他 | 其他问题导致的定位失败。|| 提示用户稍后再试。|


# 常见问题 FAQ

## Q：my.getLocation 调用失败，错误码 11，如何处理？
A：错误码 11 为表示系统定位权限未开启或未授予支付宝，如有必要，请引导开启系统权限：
* 推荐调用 [my.showAuthGuide](https://opendocs.alipay.com/mini/api/show-auth-guide) 引导用户开启权限/授权给支付宝。
* 也可使用 my.getSystemInfo 判断具体是系统未打开定位功能还是未授权支付宝，给予用户恰当的自定义提示。

## Q：my.getLocation 调用失败，错误码 2002，如何处理？
A：当 my.getLocation 触发位置授权弹窗提示时，用户勾选 “总是保持以上选择，不再询问”，点击拒绝，则会导致当次调用失败（错误码 2003)，以及后续 my.getLocation 调用直接失败（错误码 2002，即永久拒绝）。此时可行的办法：
* 尊重用户的隐私选择，在不获取位置信息的情况下，继续提供服务。
* 说明获取位置信息的必要性，然后引导用户通过右上角胶囊按钮 -> 设置，开启地理位置开关。
* 说明获取位置信息的必要性，然后调用 [my.openSetting](https://opendocs.alipay.com/mini/api/qflu8f) 帮用户打开小程序设置界面。

## Q：如何获取用户所在的省市区县名称？
A：my.getLocation 入参 type 为 1/2/3 时，接口内部会做逆地理编码，success 回调参数中包含取到省市区县名称。推荐使用 type 1，速度相对最快。

## Q：my.getLocation 在 IDE 模拟器中获取的地理位置信息不对怎么办？
A：IDE 模拟器上的 my.getLocation 默认位置为杭州。可在模拟器工具栏中点击定位按钮，自定义当前位置的经纬度：<br />![](https://img.alicdn.com/imgextra/i1/O1CN01jQG0oE1ZOJqojXjqo_!!6000000003184-0-tps-456-266.jpg)。

## Q：my.getLocation 返回的行政区划名称和编码的完整数据在哪里下载？
A：当前使用的行政区数据可[点此下载](https://gw.alipayobjects.com/os/bmw-prod/14ef43d2-dc0d-447d-9f75-ac6c784ae10e.xlsx)。此数据与民政部公布的 [2019年中华人民共和国行政区划代码](https://www.mca.gov.cn/article/sj/xzqh/1980/202002/20200200025008.shtml) 基本一致。
