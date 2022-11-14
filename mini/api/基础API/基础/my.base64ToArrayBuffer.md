# 简介

**my.base64ToArrayBuffer** 将 Base64 字符串转成 ArrayBuffer 对象。

# 使用限制

- 基础库 [2.7.3](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 或更高版本。若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码

```javascript
const base64 = 'CxYh';
const arrayBuffer = my.base64ToArrayBuffer(base64);
console.log(arrayBuffer.byteLength)
```

## 入参

类型为 `String`，代表要转换成 ArrayBuffer 对象的 Base64 字符串。

## 返回值

类型为 `ArrayBuffer` 对象，其属性如下：

| **属性** | **类型** | **描述**             |
| -------- | -------- | -------------------- |
| byteLength    | Number   | 二进制数据缓冲区长度。 |
