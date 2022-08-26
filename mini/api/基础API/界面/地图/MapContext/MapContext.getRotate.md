# 简介

**MapContext.getRotate** 用于获取当前地图的旋转角。

## 使用限制

- 基础库 [2.6.2](https://opendocs.alipay.com/mini/01iq3i) 或更高版本；支付宝客户端 10.2.0 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码

```javascript
// .js
this.mapCtx = my.createMapContext('map');
this.mapCtx.getRotate({
  success: res => {
    console.log(res.rotate);
  },
});
```

## 入参

Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述**             |
| -------- | -------- | -------- | -------------------- |
| success  | Function | 否       | 调用成功的回调函数。 |

### Function success

success 回调函数会携带一个 Object 类型的对象，其属性如下：

| **属性** | **类型** | **描述** |
| -------- | -------- | -------- |
| rotate   | Number   | 旋转角。 |
