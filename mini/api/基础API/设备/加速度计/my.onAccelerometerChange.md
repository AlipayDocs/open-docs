# 简介

**my.onAccelerometerChange** 是监听加速度数据的 API，回调间隔为 500ms，接口调用后会自动开始监听，可使用 [my.offAccelerometerChange()](/mini/api/kape7p)停止监听。

## 使用限制

- 基础库 [1.9.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.32 或更高版本，若版本较低，建议采取 [兼容处理](/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

```javascript
// .js
my.onAccelerometerChange(function (res) {
  console.log(res.x);
  console.log(res.y);
  console.log(res.z);
});
```

## 入参

入参为 Function(callback) 类型，callback 回调函数的参数类型为 Object 类型，属性如下：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| x | Number | X 轴 |
| y | Number | Y 轴 |
| z | Number | Z 轴 |
| timestamp | Number | 时间戳。<br />基础库 [2.7.5](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2)、支付宝客户端 10.2.30 及以上支持。 |
