# 简介

**my.onAppShow** 是监听小程序切前台事件的 API。该事件与框架 [app.js 注册小程序](https://opendocs.alipay.com/mini/framework/app-detail) 时 `onShow` 的回调时机一致。对应的取消监听 API 请参见 [my.offAppShow](https://opendocs.alipay.com/mini/api/tkohmw)。

## 使用限制

- 基础库 [1.20.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.68 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 由于开发者工具版本限制，目前本 API 暂不支持在开发者工具调试和真机调试，仅支持真机预览。开发者请调至 **预览** 模式，在支付宝客户端扫码查看效果。
- 请勿使用 API 监听匿名函数，否则将无法关闭监听。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码

```javascript
//app.js

my.onAppShow(function(res) {
  console.log('appShow:', res)
})

App({
 
})
```

## 入参

入参为回调函数： 

| **参数** | **类型** | **描述** | 
| --- | --- | --- | 
| 回调函数 | Function | 小程序切前台事件的回调函数。 |

### 回调函数接收的参数是一个对象，其属性如下：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| path | string | 当前小程序的页面地址，从启动参数 page 字段解析而来，page 忽略时默认为首页。 |
| scene | number | 启动小程序的 [场景值](https://opendocs.alipay.com/mini/framework/scene)。 |
| query | Object | 当前小程序的 query，从启动参数的 query 字段解析而来，解析规则可查看 [小程序全局 / 页面参数设置以及解析细节](https://opendocs.alipay.com/mini/03durs)。 |
| apiCategory | string | API 类别，基础库 **2.7.22** 开始支持。 |
