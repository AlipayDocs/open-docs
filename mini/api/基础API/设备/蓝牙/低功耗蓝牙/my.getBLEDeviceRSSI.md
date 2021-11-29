
# 简介
获取蓝牙低功耗设备的信号强度（Received Signal Strength Indication, RSSI）。

# 使用限制

- 基础库 [1.24.6](https://opendocs.alipay.com/mini/framework/lib) 或更高版本。若版本较低，建议采取 [兼容处理](https://docs.alipay.com/mini/framework/compatibility)。
- 此 API 暂仅支持企业支付宝小程序使用。

# 接口调用

## 入参
Object 类型，属性如下：

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| deviceId | String | 是 | 蓝牙设备 id，参考 device 对象。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |


### success 返回值
| **属性** | **类型** | **描述** |
| --- | --- | --- |
| RSSI | Number | 信号强度，单位 dBm。 |

