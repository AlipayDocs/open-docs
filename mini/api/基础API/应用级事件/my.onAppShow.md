# 简介

**my.onAppShow** 监听小程序切前台事件。

实质为动态注册 [App.onShow](https://opendocs.alipay.com/mini/framework/app-detail) 生命周期回调。对应的取消监听接口为 [my.offAppShow](https://opendocs.alipay.com/mini/api/tkohmw)。


## 使用限制

- 基础库 [1.20.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.68 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 由于开发者工具版本限制，目前本 API 暂不支持在开发者工具调试和真机调试，仅支持真机预览。开发者请调至 **预览** 模式，在支付宝客户端扫码查看效果。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码

```javascript
my.onAppShow(function(res) {
  console.log('appShow:', res)
})
```

## 入参

Function callback(object) 小程序切前台事件的回调函数。

回调参数为一个 Object，包含以下属性：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| path | string | 当前小程序的页面地址，从启动参数 page 字段解析而来，page 忽略时默认为首页。 |
| scene | number | 启动小程序的 [场景值](https://opendocs.alipay.com/mini/framework/scene)。 |
| query | Object | 当前小程序的 query，从启动参数的 query 字段解析而来，解析规则可查看 [小程序全局 / 页面参数设置以及解析细节](https://opendocs.alipay.com/mini/03durs)。 |
| apiCategory | string | API 类别，基础库 **2.7.22** 开始支持。 |
