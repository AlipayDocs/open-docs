# 简介
**my.startBeaconDiscovery** 是开始搜索附近的 iBeacon 设备的 API。

## 使用限制

- 支付宝客户端 10.1.8 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。 
- 此 API 暂仅支持企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码
```javascript
// .js
my.startBeaconDiscovery({
  uuids:['uuid1','uuid2'],
  success: (res) => {
    console.log(res)
  },
  fail:(res) => {
  },
  complete: (res)=>{
  }
});
```

## 入参
Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| uuids | StringArray | 是 | 目标 iBeacon 设备广播的 UUIDs。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

**说明**：

- uuid1、uuid2 为目标 iBeacon 的 UUID，可从硬件厂商获取，如果为空，无法搜索到 iBeacon。<br />
- iBeacon 需要位置权限。iOS 11 及以后版本的手机，通过手机控制中心的快捷开关打开蓝牙，无法使用 iBeacon，需要在 设置 > 蓝牙 中开启蓝牙，方可使用。<br />
- 建议在 [my.onBeaconUpdate](https://opendocs.alipay.com/mini/api/kvdg9y) 回调中处理发现到的 iBeacon 设备信息。<br />

### Function fail

fail 回调函数会携带一个 Object 类型的对象，其属性如下：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| error | String | 错误码。 |
| errorMessage | String | 错误信息。 |


## 错误码
| **错误码** | **描述** | **说明** |
| --- | --- | --- |
| 11000 | unsupport | 系统或设备不支持。 |
| 11001 | bluetooth invalid | 蓝牙服务不可用。 |
| 11002 | location service unavailable | 位置服务不可用。 |
| 11003 | location authorization forbidden | 位置服务权限禁止。 |
| 11004 | already discovering | 已经开始搜索。 |
| 11006 | uuid invalid | UUID 格式错误。 |
| 11008 | uuids empty | 参数错误，UUID 数组为空。 |
