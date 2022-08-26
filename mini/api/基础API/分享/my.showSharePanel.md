# 简介

**my.showSharePanel** 是唤起分享面板的 API。

当通过 my.showSharePanel 唤起分享功能时，[page.onShareAppMessage](https://opendocs.alipay.com/mini/framework/page-detail#%E9%A1%B5%E9%9D%A2%E4%BA%8B%E4%BB%B6%E5%A4%84%E7%90%86%E5%87%BD%E6%95%B0) 入参中 `from` 的值为 `code`。

## 使用限制

基础库 [1.17.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.60 或更高版本，若版本较低，建议采取 [兼容处理](/mini/framework/compatibility)。

此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## .js 示例代码

```javascript
// .js
my.showSharePanel();
```
