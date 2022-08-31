# 简介

获取蓝牙低功耗设备的信号强度（Received Signal Strength Indication, RSSI）。

# 使用限制

- 基础库 [1.24.6](https://opendocs.alipay.com/mini/framework/lib) 或更高版本。若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 暂仅支持企业支付宝小程序使用。

# 接口调用

## 入参

Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| deviceId | String | 是 | 蓝牙设备 ID。Android 上为设备 MAC 地址，iOS 上为设备 UUID。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

### Function success

success 回调函数会携带一个 Object 类型的对象，其属性如下：

| **属性** | **类型** | **描述**             |
| -------- | -------- | -------------------- |
| RSSI     | Number   | 信号强度，单位 dBm。 |
