# 简介

**my.onBeaconUpdate** 是监听 iBeacon 设备的更新事件的 API。

## 使用限制

- 支付宝客户端 10.1.8 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 暂仅支持企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码

```javascript
// .js
const callback = (res) => {
  console.log("回调函数",res)
}
my.onBeaconUpdate(callback);
```

## 入参

入参为回调函数：

| **参数** | **类型** | **必填** | **描述**                                |
| -------- | -------- | -------- | --------------------------------------- |
| callback  | Function | 否       | 监听 iBeacon 设备的更新事件的回调函数。 |

### Function success

callback 回调函数会携带一个 Object 类型的对象，其属性如下：

| **属性** | **类型**    | **描述**                            |
| -------- | ----------- | ----------------------------------- |
| beacons  | ObjectArray | 当前搜寻到的所有 iBeacon 设备列表。 |

#### ObjectArray beacons

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| uuid | String | iBeacon 设备广播的 UUID。 |
| major | String | iBeacon 设备的主 ID。 |
| minor | String | iBeacon 设备的次 ID。 |
| proximity | Number | 表示设备距离的枚举值（0-3 分别代表：未知、极近、近、远）。 |
| accuracy | Number | iBeacon 设备的距离。 |
| rssi | Number | iBeacon 信号强度。 |

## 错误码

| **错误码** | **描述**                         | **说明**                  |
| ---------- | -------------------------------- | ------------------------- |
| 11000      | unsupport                        | 系统或设备不支持。        |
| 11001      | bluetooth invalid                | 蓝牙服务不可用。          |
| 11002      | location service unavailable     | 位置服务不可用。          |
| 11003      | location authorization forbidden | 位置服务权限禁止。        |
| 11004      | already discovering              | 已经开始搜索。            |
| 11006      | uuid invalid                     | UUID 格式错误。          |
| 11008      | uuids empty                      | 参数错误，UUID 数组为空。 |

