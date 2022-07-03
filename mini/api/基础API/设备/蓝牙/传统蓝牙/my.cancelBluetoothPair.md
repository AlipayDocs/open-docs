# 简介
**my.cancelBluetoothPair** 是取消蓝牙配对的 API。

## 使用限制

- 当前仅支持 Android 系统。
- 基础库 [2.7.2](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 或更高版本；支付宝客户端 10.2.0 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 暂仅支持企业支付宝小程序使用。

# 接口调用

## 示例代码
```javascript
//.js

my.cancelBluetoothPair({
  deviceId: '', // 蓝牙设备 id
  success: (res) => {
    my.alert({ content: "success:"+ JSON.stringify(res) });
  },
  fail: (error) => {
    my.alert({ content: "fail:"+ JSON.stringify(res) });
  }
 });
```

## 入参
Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| deviceId | String | 是 | 蓝牙设备 id。 |
| success | Function | 否 | 接口调用成功的回调函数。 |
| fail | Function | 否 | 接口调用失败的回调函数。 |
| complete | Function | 否 | 接口调用结束的回调函数（调用成功、失败都会执行）。 |
