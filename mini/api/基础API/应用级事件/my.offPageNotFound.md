
# 简介
**my.offPageNotFound** 是取消监听小程序要打开的页面不存在事件的 API。

## 使用限制

- 基础库 [2.7.2](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 或更高版本。若版本较低，建议采取 [兼容处理](https://docs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码
```javascript
//.js
function handlePageNotFound(res) {
  my.redirectTo({
    url: 'pages/...'
  }); // 如果是 tabbar 页面，请使用 my.switchTab
}
my.onPageNotFound(handlePageNotFound);
my.offPageNotFound(handlePageNotFound);
```

## 入参
入参为回调函数：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| 回调函数 | Function | 小程序要打开的页面不存在事件的回调函数。 |

