
# 简介
设置低功耗蓝牙设备的最大传输单元（Maximum Transmission Unit, MTU）。需在 [my.connectBLEDevice](https://opendocs.alipay.com/mini/api/tmew6e) 调用成功后调用，mtu 设置范围（22,512）。

# 使用限制

- 安卓5.1以上有效，iOS 因系统限制不支持。
- 基础库 [1.24.6](https://opendocs.alipay.com/mini/framework/lib) 或更高版本。若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 暂仅支持企业支付宝小程序使用。

# 接口调用

## 入参

Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| deviceId | String | 是 | 蓝牙设备 id，参考 device 对象。 |
| mtu | Number | 是 | 最大传输单元(22,512) 区间内，单位 bytes。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |


### Function success

success 回调函数会携带一个 Object 类型的对象，其属性如下：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| mtu | number | 最终协商的 MTU 值，与传入参数一致。安卓客户端 8.0.9 开始支持。 |

