# 简介

获取低功耗蓝牙设备的最大传输单元（Maximum Transmission Unit, MTU）。

# 使用限制

- 支付宝客户端 10.2.30 版本，基础库 [2.7.7](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 或更高版本开始支持。若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
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

### Funtion success

success 回调函数会携带一个 Object 类型的对象，其属性如下：

| **属性** | **类型** | **描述**     |
| -------- | -------- | ------------ |
| mtu      | Number   | 外设的 MTU。 |
