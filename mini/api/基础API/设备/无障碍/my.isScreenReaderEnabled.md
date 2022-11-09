## 简介

获取设备是否开启视觉无障碍模式。

## 使用限制

- 支付宝客户端 10.1.87 版本，**基础库** [1.23.4](https://opendocs.alipay.com/mini/framework/compatibility) 开始支持，低版本需要做 [兼容处理](https://docs.alipay.com/mini/framework/compatibility)。
- 此 API 暂仅支持企业支付宝小程序使用。

## 接口调用

### 示例代码

#### .js 示例代码

```javascript
my.isScreenReaderEnabled({
  success(res) {
    if (res && res.screenReaderEnabled) {
      console.log('当前设备处于无障碍模式下');
    }
  },
});
```

## 入参

Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

### Function success

success 回调函数会携带一个 Object 类型的对象，其属性如下：

| **属性**            | **类型** | **描述**           |
| ------------------- | -------- | ------------------ |
| screenReaderEnabled | Boolean  | 是否开启无障碍模式 |
