
# 简介
**my.getSystemInfoSync** 是获取手机系统信息的同步接口。返回值同 [my.getSystemInfo](api/system-info) 接口 success 回调函数。<br />如果只需获取 **clientName**、**clientVersion**、**language**、**platform** 字段，推荐使用更加轻量化的 [my.env](https://opendocs.alipay.com/mini/api/env) API。

## 使用限制

- 该接口是同步接口，有超时的判断。当超时后，接口将返回 undefined。<br />
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。<br />

## 扫码体验
![](https://gw.alipayobjects.com/zos/skylark-tools/public/files/c41f07c34dc902ff60df5d282d248190.png#align=left&display=inline&height=158&margin=%5Bobject%20Object%5D&originHeight=158&originWidth=128&status=done&style=none&width=128)

## 效果示例
![](https://gw.alipayobjects.com/zos/skylark-tools/public/files/c11e1d00bdb3443f20011e0fd2e252f6.gif#align=left&display=inline&height=525&margin=%5Bobject%20Object%5D&originHeight=525&originWidth=300&status=done&style=none&width=300)

# 接口调用

## 示例代码

### .json  示例代码
```json
// API-DEMO page/API/get-system-info/get-system-info.json
{
    "defaultTitle": "获取手机系统信息"
}
```

### .axml 示例代码
```html
<!-- API-DEMO page/API/get-system-info/get-system-info.axml-->
<view class="page">
  <view class="page-section">
    <view class="page-section-demo">
      <text>手机型号</text>
      <input type="text" disabled="{{true}}" value="{{systemInfo.model}}"></input>
    </view>
    <view class="page-section-demo">
      <text>语言</text>
      <input type="text" disabled="{{true}}" value="{{systemInfo.language}}"></input>
    </view>
    <view class="page-section-demo">
      <text>版本</text>
      <input type="text" disabled="{{true}}" value="{{systemInfo.version}}"></input>
    </view>
    <view class="page-section-demo">
      <text>window宽度</text>
      <input type="text" disabled="{{true}}" value="{{systemInfo.windowWidth}}"></input>
    </view>
    <view class="page-section-demo">
      <text>window高度</text>
      <input type="text" disabled="{{true}}" value="{{systemInfo.windowHeight}}"></input>
    </view>
    <view class="page-section-demo">
      <text>DPI</text>
      <input type="text" disabled="{{true}}" value="{{systemInfo.pixelRatio}}"></input>
    </view>
    <view class="page-section-btns">
      <view onTap="getSystemInfo">获取手机系统信息</view>
      <view onTap="getSystemInfoSync">同步获取手机系统信息</view>
    </view>
  </view>
</view>
```

### .js 示例代码
```javascript
// API-DEMO page/API/get-system-info/get-system-info.js
Page({
  data: {
    systemInfo: {}
  },
  getSystemInfo() {
    my.getSystemInfo({
      success: (res) => {
        this.setData({
          systemInfo: res
        })
      }
    })
  },
  getSystemInfoSync() {
    this.setData({
      systemInfo: my.getSystemInfoSync(),
    });
  },
})
```
