# 简介

**my.onBeaconServiceChange** 是监听 iBeacon 服务的状态变化的 API。

## 使用限制

- 支付宝客户端  10.1.8 或更高版本，若版本较低，建议采取 [兼容处理](/mini/framework/compatibility)。
- iOS 11 及之后版本 “控制中心蓝牙开关” 和 “设置 > 蓝牙 > 开关” 分离，控制中心蓝牙开关不再影响 iBeacon 使用，但是  my.onBeaconServiceChange  事件仍然会回调，建议 iOS 11 之后版本调用该事件回调后，继续等待  [my.onBeaconUpdate](https://opendocs.alipay.com/mini/api/kvdg9y)  以确认是否提示用户开启蓝牙。
- 此 API 暂仅支持企业支付宝小程序使用。

# 接口调用

## 示例代码

```javascript
// .js
my.onBeaconServiceChange(res => {});
```

## 入参

入参为回调函数：

| **属性** | **类型** | **描述**                                |
| -------- | -------- | --------------------------------------- |
| 回调函数 | Function | 监听 iBeacon 服务的状态变化的回调函数。 |

### 回调参数

| **属性**    | **类型** | **描述**               |
| ----------- | -------- | ---------------------- |
| available   | Boolean  | 服务目前是否可用。     |
| discovering | Boolean  | 目前是否处于搜索状态。 |

## 错误码

| **错误码** | **描述**                         | **说明**                  |
| ---------- | -------------------------------- | ------------------------- |
| 11000      | unsupport                        | 系统或设备不支持。        |
| 11001      | bluetooth invalid                | 蓝牙服务不可用。          |
| 11002      | location service unavailable     | 位置服务不可用。          |
| 11003      | location authorization forbidden | 位置服务权限禁止。        |
| 11004      | already discovering              | 已经开始搜索。            |
| 11006      | uuid invalid                     | UUID 格式错误。           |
| 11008      | uuids empty                      | 参数错误，UUID 数组为空。 |
