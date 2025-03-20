# 简介

**my.getSystemInfo** 是获取手机系统信息的 API。

如果只需获取 **clientName**、**clientVersion**、**language**、**platform** 字段，推荐使用更加轻量化的 [my.env](https://opendocs.alipay.com/mini/api/env)。

## 使用限制

此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验

![](https://gw.alipayobjects.com/zos/skylark-tools/public/files/fcf5eb6913c727b207a27d2a9d383362.png#align=left&display=inline&height=158&margin=%5Bobject%20Object%5D&originHeight=158&originWidth=128&status=done&style=none&width=128)

# 接口调用

## 示例

[小程序在线](https://opendocs.alipay.com/openbox/mini/opendocs/get-system-info?view=preview&defaultPage=pages/index/index&defaultOpenedFiles=pages/index/index&theme=light)

### .js 示例代码

```javascript
// get-system-info.js
Page({
  data: {
    systemInfo: {},
  },
  getSystemInfo() {
    my.getSystemInfo({
      success: res => {
        this.setData({
          systemInfo: res,
        });
      },
    });
  },
  // 对等的同步接口
  getSystemInfoSync() {
    this.setData({
      systemInfo: my.getSystemInfoSync(),
    });
  },
});
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
| windowWidth | Number | 可使用窗口宽度。单位：px |
| windowHeight | Number | 可使用窗口高度。 单位：px <br> **注** ：“可使用”是指除去 statusBar 和 titleBar 后可以自定义内容的区域。 |
| language | String | 支付宝设置的语言。<br />分别有以下值：zh-Hans（简体中文）、en（English）、zh-Hant（繁体中文（台湾））、zh-HK（繁体中文（香港））。 |
| version | String | 支付宝版本号。 |
| storage | String | 设备磁盘容量。 |
| currentBattery | String | 当前电量百分比。 |
| system | String | 系统版本。 |
| platform | String | 系统名：Android，iOS / iPhone OS。 |
| titleBarHeight | Number | 标题栏高度。 |
| statusBarHeight | Number | 状态栏高度。单位：px |
| screen | Object | 屏幕宽度和高度。结构为： { width: Number, height: Number } 单位：px。 |
| screenWidth | Number | 屏幕宽度。单位：px。此属性在 Android 上取值有误，**建议使用 screen.width 替代。** |
| screenHeight | Number | 屏幕高度。单位：px。此属性在 Android 上取值有误，**建议使用 screen.height 替代。** |
| safeArea | Object | 在竖屏正方向下的安全区域。单位：px。|
| safeArea | Object | 在竖屏正方向下的安全区域插入位置。单位：px。|
| brand | String | 手机品牌。 |
| fontSizeSetting | Number | 用户设置字体大小。单位：px |
| app | String | 当前运行的客户端。若当前为支付宝，则有效值为 "alipay"。不同的客户端，对应的有效值如下：<ul><li>alipay：支付宝。</li><li>UC：UC 浏览器。</li><li>QUARK：夸克浏览器。</li><li>AK：阿里健康。</li><li>amap：高德。</li><li>YK：优酷。</li><li>DINGTALK：钉钉。</li></ul> |

#### safeArea 返回值说明

| **手机型号**      | **类型**       | **说明**                  |
| ----------------- | -------------- | ------------------------- |
| top               | number         | 安全区域左上角纵坐标        |
| bottom            | number         | 安全区域右下角纵坐标        |
| left              | number         | 安全区域左上角横坐标        |
| right             | number         | 安全区域右下角横坐标        |
| height            | number         | 安全区域的高度             |
| width             | number         | 安全区域的宽度             |

#### safeAreaInsets 返回值说明

| **手机型号**      | **类型**       | **说明**                  |
| ----------------- | -------------- | ------------------------- |
| top               | number         | 安全区顶部插入位置         |
| bottom            | number         | 安全区底部插入位置         |
| left              | number         | 安全区域左侧插入位置        |
| right             | number         | 安全区域右侧插入位置        |

#### model 参数

对于 iPhone，model 参数将返回 iPhone 内部代码（Internal Name）。iPhone 手机型号与对应的 model 返回值如下表所示：

| **手机型号**      | **model 返回值**                  |
| ----------------- | --------------------------------- |
| iPhone            | iPhone1,1                         |
| iPhone 3G         | iPhone1,2                         |
| iPhone 3GS        | iPhone2,1                         |
| iPhone 4          | iPhone3,1 / iPhone3,2 / iPhone3,3 |
| iPhone 4S         | iPhone4,1                         |
| iPhone 5          | iPhone5,1 / iPhone5,2             |
| iPhone 5C         | iPhone5,3 / iPhone5,4             |
| iPhone 5S         | iPhone6,1 / iPhone6,2             |
| iPhone 6          | iPhone7,2                         |
| iPhone 6 Plus     | iPhone7,1                         |
| iPhone 6S         | iPhone8,1                         |
| iPhone 6S Plus    | iPhone8,2                         |
| iPhone 7          | iPhone9,1 / iPhone9,3             |
| iPhone 7 Plus     | iPhone9,2 / iPhone9,4             |
| iPhone 8          | iPhone10,1 / iPhone10,4           |
| iPhone 8 Plus     | iPhone10,2 / iPhone10,5           |
| iPhone X          | iPhone10,3 / iPhone10,6           |
| iPhone XR         | iPhone11,8                        |
| iPhone XS         | iPhone11,2                        |
| iPhone 11         | iPhone12,1                        |
| iPhone 11 Pro     | iPhone12,3                        |
| iPhone XS Max     | iPhone11,6 / iPhone11,4           |
| iPhone 11 Pro Max | iPhone12,5                        |
| iPhone 12 mini    | iPhone13,1                        |
| iPhone 12         | iPhone13,2                        |
| iPhone 12 Pro     | iPhone13,3                        |
| iPhone 12 Pro Max | iPhone13,4                        |
| iPhone SE         | iPhone14,6                        |
| iPhone 13 mini    | iPhone14,4                        |
| iPhone 13         | iPhone14,5                        |
| iPhone 13 Pro     | iPhone14,2                        |
| iPhone 13 Pro Max | iPhone14,3                        |

对于 Android 手机，因机型众多不予穷举。如有必要请按 model 的具体取值自行搜索。

# 常见问题 FAQ

## Q：my.getSystemInfo 中 screenWidth 和 screenHeight 在安卓端取值不对怎么办？

A：已知问题，Android 少除了 pixelRatio。推荐使用 screen.width 和 screen.height 代替，iOS 和 Android 一致。

## Q：my.getSystemInfo 中 windowHeight 和 screenHeight 有什么区别？

A：screenHeight 是指屏幕高度。windowHeight 是指可使用窗口高度。不设置导航栏透明时，screenHeight = windowHeight + statusBarHeight + titleBarHeight ；设置导航栏透明时，screenHeight = windowHeight 。
