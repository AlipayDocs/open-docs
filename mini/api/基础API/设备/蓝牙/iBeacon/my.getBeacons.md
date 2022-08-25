# 简介

**my.getBeacons** 是获取已经搜索到的 iBeacon 设备的 API。

## 使用限制

- 支付宝客户端  10.1.8 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- Android 在支付宝客户端 10.1.28 或之前的版本中，使用该接口返回的 rssi 值不能动态更新，建议使用事件触发方式。
- 此 API 暂仅支持企业支付宝小程序使用。

# 接口调用

## 示例代码

```javascript
// .js
my.getBeacons({
  success: res => {
    console.log(res);
  },
  fail: res => {},
  complete: res => {},
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

| **属性** | **类型**    | **描述**                    |
| -------- | ----------- | --------------------------- |
| beacons  | ObjectArray | iBeacon 设备列表。          |
| errCode  | String      | errorCode=0，接口调用成功。 |
| errorMsg | String      | 错误描述信息，成功则为 ok。 |

#### ObjectArray beacons

beacons   属性的数组由以下属性构成：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| uuid | String | iBeacon 设备广播的 UUID。 |
| major | String | iBeacon 设备的主 ID。 |
| minor | String | iBeacon 设备的次 ID。 |
| proximity | Number | 表示设备距离的枚举值（0-3 分别代表：未知、极近、近、远）。 |
| accuracy | Number | iBeacon 设备的距离。 |
| rssi | Number | iBeacon 信号强度。 |

### Function fail

fail 回调函数会携带一个 Object 类型的对象，其属性如下：

| **属性**     | **类型** | **描述**   |
| ------------ | -------- | ---------- |
| error        | String   | 错误码。   |
| errorMessage | String   | 错误信息。 |

## 错误码

| **错误码** | **说明**                         | **描述**                  |
| ---------- | -------------------------------- | ------------------------- |
| 11000      | unsupport                        | 系统或设备不支持。        |
| 11001      | bluetooth invalid                | 蓝牙服务不可用。          |
| 11002      | location service unavailable     | 位置服务不可用。          |
| 11003      | location authorization forbidden | 位置服务权限禁止。        |
| 11004      | already discovering              | 已经开始搜索。            |
| 11006      | uuid invalid                     | UUID 格式错误。           |
| 11008      | uuids empty                      | 参数错误，UUID 数组为空。 |
