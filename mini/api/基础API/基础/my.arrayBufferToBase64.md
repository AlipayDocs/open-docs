
# 简介
**my.arrayBufferToBase64** 将 ArrayBuffer 对象转成 Base64 字符串。

# 使用限制

- 基础库 [2.7.3](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 或更高版本。若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码
```javascript
const arrayBuffer = new Uint8Array([11, 22, 33])
const base64 = my.arrayBufferToBase64(arrayBuffer)
```

## 入参
类型为 `ArrayBuffer`，代表要转换成 `Base64` 字符串的 `ArrayBuffer` 对象。

### 返回值
| **属性** | **类型** | **描述** |
| --- | --- | --- |
| `Base64` 字符串 | String |  |
