# 简介
**my.showAuthGuide** 是通过权限引导模块以图文等形式向用户弹出 Dialog，引导用户打开相应的权限的 API。

权限引导的核心是引导而非权限判断，调用时机应该在业务方确认所需权限被限制的时候；此外权限引导弹框受疲劳度等因素控制。

## 使用限制

此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例

[小程序在线](https://opendocs.alipay.com/examples/cc634a7b-94dd-4f82-afd5-89fd88bcfd00) 

### .json 示例代码

```json
// API-DEMO page/API/show-auth-guide/show-auth-guide.json
{
    "defaultTitle": "权限引导"
}
```

### .axml 示例代码

```html
<!-- API-DEMO page/API/show-auth-guide/show-auth-guide.axml-->
<view class="page">
  <view class="page-description">权限引导 API</view>
  <view class="page-section">
    <view class="page-section-title">my.showAuthGuide</view>
    <view class="page-section-demo">
      <button type="primary" onTap="showAuthGuide">权限引导</button>
    </view>
  </view>
</view>
```

### .js 示例代码
```javascript
// API-DEMO page/API/show-auth-guide/show-auth-guide.js
Page({
  showAuthGuide() {
    my.showAuthGuide({ 
        authType:'LBS',
        success:(res)=>{
            //shown为true时表示会显示权限引导弹窗，为false时表示用户已经授权
            my.alert({content: '调用成功：'+JSON.stringify(res), });
        },
        fail:(error)=>{
            my.alert({content: '调用失败：'+JSON.stringify(error), });
        },
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
| 后台保活权限 | BACKGROUNDER | Android | - |
| 桌面快捷权限 | SHORTCUT | Android | - |
| 麦克风权限 | MICROPHONE | iOS | - |
| 通讯录权限 | ADDRESSBOOK | iOS | - |
| 相机权限 | CAMERA | iOS | - |
| 照片权限 | PHOTO | iOS | - |
| push 通知栏权限 | NOTIFICATION | Android | - |
| 自启动权限 | SELFSTARTING | Android | - |
| lbs 开关 | LBS | iOS / Android | - |
| 蓝牙 | BLUETOOTH | iOS / Android | 客户端 10.2.33、基础库 [2.7.10](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 开始支持。<br />可通过 `my.canIUse('showAuthGuide.object.authType.BLUETOOTH') ` 进行检测。 |
