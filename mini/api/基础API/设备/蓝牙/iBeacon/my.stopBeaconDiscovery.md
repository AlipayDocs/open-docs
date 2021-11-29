
# 简介
**my.stopBeaconDiscovery** 是停止搜索附近的 iBeacon 设备的 API。

## 使用限制

- 支付宝客户端 10.1.8 或更高版本，若版本较低，建议采取 [兼容处理](/mini/framework/compatibility)。
- 此 API 暂仅支持企业支付宝小程序使用。

# 接口调用

## .js 示例代码
```javascript
// .js
my.stopBeaconDiscovery({
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
Object 类型，属性如下：

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |


### fail 回调函数
入参为 Object 类型，属性如下：

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

