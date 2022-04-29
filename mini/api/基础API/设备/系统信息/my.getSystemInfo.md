# 简介

**my.getSystemInfo** 是获取手机系统信息的 API。

如果只需获取 **clientName**、**clientVersion**、**language**、**platform** 字段，推荐使用更加轻量化的 [my.env](https://opendocs.alipay.com/mini/api/env) API。

## 使用限制

此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验

![](https://gw.alipayobjects.com/zos/skylark-tools/public/files/fcf5eb6913c727b207a27d2a9d383362.png#align=left&display=inline&height=158&margin=%5Bobject%20Object%5D&originHeight=158&originWidth=128&status=done&style=none&width=128)

# 接口调用

## 示例

[小程序在线](https://opendocs.alipay.com/examples/e8058a45-89da-4dcb-8a7d-48f3d0640b95) 

### .json 示例代码

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

## 入参
Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

### Function success

success 回调函数会携带一个 Object 类型的对象，其属性如下：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| model | String | 手机型号。 |
| pixelRatio | Number | 设备像素比。 |
| windowWidth | Number | 窗口宽度。 |
| windowHeight | Number | 窗口高度。 |
| language | String | 支付宝设置的语言。<br />分别有以下值：zh-Hans（简体中文）、en（English）、zh-Hant（繁体中文（台湾））、zh-HK（繁体中文（香港））。 |
| version | String | 支付宝版本号。 |
| storage | String | 设备磁盘容量。<br />基础库 1.1.1 或更高版本开始支持。 |
| currentBattery | String | 当前电量百分比。<br />基础库 1.1.1 或更高版本开始支持。 |
| system | String | 系统版本。<br />基础库 1.1.1 或更高版本开始支持。 |
| platform | String | 系统名：Android，iOS / iPhone OS 。<br />基础库 1.1.1 或更高版本开始支持。 |
| titleBarHeight | Number | 标题栏高度。<br />基础库 1.1.1 或更高版本开始支持。 |
| statusBarHeight | Number | 状态栏高度。<br />基础库 1.1.1 或更高版本开始支持。 |
| screenWidth | Number | 屏幕宽度。<br />基础库 1.1.1 或更高版本开始支持。 |
| screenHeight | Number | 屏幕高度。<br />基础库 1.1.1 或更高版本开始支持。 |
| brand | String | 手机品牌。<br />基础库 1.4.0 或更高版本开始支持。 |
| fontSizeSetting | Number | 用户设置字体大小。<br />基础库 1.4.0 或更高版本开始支持。 |
| app | String | 当前运行的客户端。若当前为支付宝，则有效值为 "alipay"。不同的客户端，对应的有效值如下：<ul><li>alipay：支付宝。</li><li>UC：UC浏览器。</li><li>QUARK：夸克浏览器。</li><li>AK：阿里健康。</li><li>amap：高德。</li><li>YK：优酷。</li><li>DINGTALK：钉钉。</li></ul> |

#### model 参数
对于 iPhone，model 参数将返回 iPhone 内部代码（Internal Name）。iPhone 手机型号与对应的 model 返回值如下表所示：

| **手机型号** | **model 返回值** |
| --- | --- |
| iPhone | iPhone1,1 |
| iPhone 3G | iPhone1,2 |
| iPhone 3GS | iPhone2,1 |
| iPhone 4 | iPhone3,1 / iPhone3,2 / iPhone3,3 |
| iPhone 4S | iPhone4,1 |
| iPhone 5 | iPhone5,1 / iPhone5,2 |
| iPhone 5C | iPhone5,3 / iPhone5,4 |
| iPhone 5S | iPhone6,1 / iPhone6,2 |
| iPhone 6 | iPhone7,2 |
| iPhone 6 Plus | iPhone7,1 |
| iPhone 6S | iPhone8,1 |
| iPhone 6S Plus | iPhone8,2 |
| iPhone 7 | iPhone9,1 / iPhone9,3 |
| iPhone 7 Plus | iPhone9,2 / iPhone9,4 |
| iPhone 8 | iPhone10,1 / iPhone10,4 |
| iPhone 8 Plus | iPhone10,2 / iPhone10,5 |
| iPhone X | iPhone10,3 / iPhone10,6 |
| iPhone XR | iPhone11,8 |
| iPhone XS | iPhone11,2 |
| iPhone 11 | iPhone12,1 |
| iPhone 11 Pro | iPhone12,3 |
| iPhone XS Max | iPhone11,6 / iPhone11,4 |
| iPhone 11 Pro Max | iPhone12,5 |
| iPhone 12 mini | iPhone13,1 |
| iPhone 12 | iPhone13,2 |
| iPhone 12 Pro | iPhone13,3 |
| iPhone 12 Pro Max | iPhone13,4 |

