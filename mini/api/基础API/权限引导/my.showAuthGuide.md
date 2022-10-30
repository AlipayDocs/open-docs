# 简介

**my.showAuthGuide** 弹出图文提示对话框，引导用户打开并授予支付宝指定权限。

小程序中的部分 API（如 my.chooseImage、my.chooseLocation 等）或功能涉及手机上特定设备/隐私数据的使用，需要用户在系统设置里开启相关功能/授权给支付宝。如果相关权限缺失，而该权限对于小程序的使用又不可缺少，建议使用 my.showAuthGuide 给予用户引导。

调用 my.showAuthGuide 时，如果指定的权限类型已被授予，在 iOS 上不会再次弹出引导，但在 Android 的某些版本/机型上针对部分权限每次都会弹出引导。因而，请先通过 [my.getSystemInfo](https://opendocs.alipay.com/mini/api/system-info) 判断权限开启/授予情况，或在目标 API 调用失败以后，再酌情调用 my.showAuthGuide。

此外，my.chooseImage 等 API 的成功调用也依赖用户在支付宝里授权给当前小程序，相关内容可参考 [my.getSetting](https://opendocs.alipay.com/mini/api/xmk3ml) 文档简介部分的描述。

## 使用限制

此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例

[小程序在线](https://opendocs.alipay.com/openbox/mini/opendocs/show-auth-guide?view=preview&defaultPage=pages/index/index&defaultOpenedFiles=pages/index/index&theme=light)

### 示例代码

```javascript
Page({
  // 示例一 先判断再调用
  getLocationExample1() {
    my.getSystemInfo({
      success(res) {
        if (res.locationEnabled && res.locationAuthorized) {
          my.getLocation({
            complete: (res) => my.alert({ title: "getLocation compete", content: JSON.stringify(res)}),
          });
        } else {
          console.log(res.locationEnabled ？ "定位权限未授予支付宝" : "定位功能未开启");
          my.showAuthGuide({ authType: "LBS" });
        }
      }
    });
  },
  
  // 示例二 失败后再引导
  getLocationExample2() {
    my.getLocation({
      success: (res) => my.alert({ title: "getLocation success", content: JSON.stringify(res) }),
      fail: (res) => {
        if (res.error == 11) {
          console.log("定位功能未开启或定位权限未授予支持宝");
          my.showAuthGuide({ authType: "LBS" });
        } else {
          my.alert({ title: 'getLocation fail', content: JSON.stringify(res) });
        }
      }
    });
  },
});
```

## 入参

入参为 Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| authType | String | 是 | 引导的权限标识，用于标识该权限类型，详情可查看 **支持的 authType**。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

### 支持的 authType

| **权限名称** | **权限码** | **支持平台** | **描述** |
| --- | --- | --- | --- |
| 相机 | CAMERA | iOS / Android | - |
| 照册 | PHOTO | iOS | - |
| 地理位置 | LBS | iOS / Android | - |
| 蓝牙 | BLUETOOTH | iOS / Android | 客户端 10.2.33、基础库 2.7.10 开始支持。<br />可通过 `my.canIUse('showAuthGuide.object.authType.BLUETOOTH')` 检测。 |
| 麦克风 | MICROPHONE | iOS / Android | - |
| 通讯录 | ADDRESSBOOK | iOS / Android | - |
| push 通知栏权限 | NOTIFICATION | iOS / Android | - |
| 后台保活 | BACKGROUNDER | Android | - |
| 创建桌面快捷方式 | SHORTCUT | Android | 部分机型系统设置中没有“创建桌面快捷方式”选项，一般为默认有权限或者使用时询问用户。 |

### success 回调

success 回调会收到 Object 类型的参数，基属性如下：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| shown | Boolean | 是否已显示引导授权弹框。<br>**注意**：当前 Android 上实现有缺陷，shown 始终为 true，并不能反映实际情况。 |

## 错误码

| **错误码** | **描述**   | **解决方案**                       |
| ---------- | ---------- | ---------------------------------- |
| 2          | 参数错误。 | 请使用文档中提供的 authType 选项。 |
