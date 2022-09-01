# 简介

**my.makeBluetoothPair** 是蓝牙配对接口。连接蓝牙之前，部分设备需要先配对。

## 使用限制

- 暂仅安卓系统支持此功能。
- 基础库 [2.6.2](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 或更高版本；支付宝客户端 10.2.0 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 暂仅支持企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码

```javascript
my.makeBluetoothPair({
  deviceId: '', //蓝牙设备id。
  pin: '', //pin 码。
  timeout: 20, //超时时间，默认为 20s。
  success: res => {
    my.alert({ content: 'success:' + JSON.stringify(res) });
  },
  fail: error => {
    my.alert({ content: 'fail:' + JSON.stringify(error) });
  },
});
```

## 入参

Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| deviceId | String | 是 | 蓝牙设备 id。 |
| pin | ArrayBuffer | 否 | pin 码。 |
| timeout | Number | 否 | 超时时间。默认值为 20 S（秒）。 |
| success | Function | 否 | 接口调用成功的回调函数。 |
| fail | Function | 否 | 接口调用失败的回调函数。 |
| complete | Function | 否 | 接口调用结束的回调函数（调用成功、失败都会执行）。 |
