# 简介

**my.onPageNotFound** 是监听小程序要打开的页面不存在事件的 API。该事件与 [App.onPageNotFound](https://opendocs.alipay.com/mini/framework/app-detail#object%20%E5%B1%9E%E6%80%A7%E8%AF%B4%E6%98%8E) 的回调时机一致。

## 使用限制

- 基础库 [2.7.2](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 或更高版本。若版本较低，建议采取 [兼容处理](https://docs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 注意事项

- 开发者可以在回调中进行页面重定向，但必须在回调中同步处理，异步处理（例如 setTimeout 异步执行）无效。
- 若开发者没有调用 my.onPageNotFound 绑定监听，也没有声明 **App.onPageNotFound**，当跳转页面不存在时，将推入支付宝原生的 **页面不存在** 提示页面。
- 回调中重定向的页面必须是已经加载好资源的页面，如果是未加载的分包页面和插件页面，运行时会报错，无法完成重定向。
- 如果回调中又重定向到另一个不存在的页面，将推入支付宝原生的 **页面不存在** 提示页面，并且不再第二次回调。
- 仅响应小程序冷启动或热启动时的页面找不到事件，不支持处理 [路由 API](https://opendocs.alipay.com/mini/api/fu8l65) 的失败场景。

# 接口调用

## 示例代码

### .js 示例代码

```javascript
//app.js
my.onPageNotFound(res => {
  my.redirectTo({
    url: '/pages/...',
  }); // 如果是 tabbar 页面，请使用 my.switchTab
});

App({
})
```

## 入参

入参为回调函数：

| **参数** | **类型** | **描述**                                 |
| -------- | -------- | ---------------------------------------- |
| 回调函数 | Function | 小程序要打开的页面不存在事件的回调函数。 |

### 回调函数

| **属性** | **类型** | **说明** |
| --- | --- | --- |
| path | String | 不存在页面的路径（代码包路径）。 |
| query | Object | 打开不存在页面的 query 参数。 |
| isEntryPage | Boolean | 是否本次启动的首个页面（例如从分享等入口进来，首个页面是开发者配置的分享页面）。 |
