
# 简介
**my.getAppIdSync** 是同步获取小程序 APPID 的API。

## 使用限制

- 基础库 [1.20.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.68 或更高版本，若版本较低，建议采取 [兼容处理](/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码
```javascript
const appIdRes = my.getAppIdSync();
console.log(appIdRes.appId);
```

## 返回值
| **属性** | **类型** | **描述** |
| --- | --- | --- |
| appId | String | 当前小程序的 APPID。 |



