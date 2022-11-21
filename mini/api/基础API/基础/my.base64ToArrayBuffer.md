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
```

## 入参

类型为 `String`，代表要转换成 ArrayBuffer 对象的 Base64 字符串。

## 返回值

类型为 `ArrayBuffer` 对象。

## Bug & Tip

- `Bug` iOS 中，接口返回值在控制台打印为 ArrayBuffer {}，实际上是转换成功的，可以通过打印 byteLength 属性确认。
