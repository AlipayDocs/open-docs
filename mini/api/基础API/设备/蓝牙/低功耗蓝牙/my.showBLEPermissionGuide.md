# 简介

**my.showBLEPermissionGuide** 是蓝牙统一授权/开关引导流程的 API。

## 使用限制

- 支付宝客户端 10.2.38，基础库 [2.7.11](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 开始支持，低版本需要做 [兼容处理](https://docs.alipay.com/mini/framework/compatibility)。
- 此 API 暂仅支持企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码

```javascript
my.showBLEPermissionGuide（{
 firstTipsTitle: "首次使用蓝牙业务提示弹窗标题", //仅iOS有效，建议不配置
 firstTipsMessage: "首次使用蓝牙业务提示弹窗内容", //仅iOS有效，建议不配置
 authTipsTitle:" 开启蓝牙授权弹窗标题", //仅iOS有效，建议不配置
 authTipsMessage: "开启蓝牙授权弹窗业务提示内容", //仅iOS有效，建议不配置
 authTipsButton: "去开启", //仅iOS有效，建议不配置
 openTipsTitle: "开启蓝牙开关弹窗标题", //仅iOS有效，建议不配置
 openTipsMessage: "开启蓝牙开关弹窗业务提示内容", //仅iOS有效，建议不配置
 openTipsButton: "去开启", //仅iOS有效，建议不配置
  bizType: "bizType", //仅Android有效
  success: (res) => {
    console.log(res)
  },
  fail: (err) => {
    console.error("getBLEDeviceStatus:"+JSON.stringify(err))
  }
})
```

## 入参

Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| firstTipsTitle | String | 否 | 蓝牙首次使用，业务提示弹窗标题（仅 iOS 有效，不配置则不会弹窗）。 |
| firstTipsMessage | String | 否 | 蓝牙首次使用，业务提示弹窗内容（仅 iOS 有效，不配置则不会弹窗）。 |
| authTipsTitle | String | 否 | 授权蓝牙，业务提示弹窗标题（仅 iOS 有效，不配置则不会弹窗）。 |
| authTipsMessage | String | 否 | 授权蓝牙，业务提示弹窗内容（仅 iOS 有效，不配置则不会弹窗）。 |
| authTipsButton | String | 否 | 授权蓝牙，业务提示弹窗按钮标题（仅 iOS 有效，不配置则不会弹窗）。 |
| openTipsTitle | String | 否 | 开启蓝牙，业务提示弹窗标题。 |
| openTipsMessage | String | 否 | 开启蓝牙，业务提示弹窗内容。 |
| openTipsButton | String | 否 | 开启蓝牙，业务提示弹窗按钮标题。 |
| bizType | String | 是 | 仅 Android 有效。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

### Function success

success 回调函数会携带一个 Object 类型的对象，其属性如下：

| **属性** | **类型** | **描述**                |
| -------- | -------- | ----------------------- |
| success  | Boolean  | true 表示蓝牙完全可用。 |

## 错误码

| **错误码** | **描述**                       |
| ---------- | ------------------------------ |
| 60000      | auth or open status unknow!    |
| 60001      | auth ble status unknow!        |
| 60002      | open ble status unknow!        |
| 60003      | request authorize tips denied! |
| 60004      | request authorize sys denied!  |
| 60005      | request open ble denied!       |
| 60006      | request auth ble denied!       |
| 60008      | internal error！               |
| 60009      | lbs service forbidden!         |
| 60010      | do not support ble!            |
