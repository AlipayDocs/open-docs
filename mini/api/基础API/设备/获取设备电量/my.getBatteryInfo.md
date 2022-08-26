# 简介

**my.getBatteryInfo** 是用于获取电量的异步接口。无需传入参，异步获取当前设备的电量和充电状态。

## 使用限制

- 基础库 [1.12.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.38 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 暂仅支持企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码

```javascript
// .js
my.getBatteryInfo({
  success: res => {
    my.alert({ content: '系统信息：' + JSON.stringify(res) });
    console.log({ content: '系统信息：' + JSON.stringify(res) });
  },
  fail: error => {
    my.alert({ content: '获取失败' + JSON.stringify(error) });
  },
  complete: () => {
    my.alert({ title: 'complete回调' });
  },
});
```

## 入参

Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| success | Function | 否 | 接口调用成功的回调函数。 |
| fail | Function | 否 | 接口调用失败的回调函数。 |
| complete | Function | 否 | 接口调用结束的回调函数（调用成功、失败都会执行）。 |

### Function success

success 回调函数会携带一个 Object 类型的对象，其属性如下：

| **属性**   | **类型** | **描述**             |
| ---------- | -------- | -------------------- |
| level      | Int      | 当前设备电量。       |
| isCharging | Boolean  | 当前设备是否充电中。 |
