
# 简介
**my.getStorage** 是获取缓存数据的异步接口。


小程序缓存默认具有支付宝账号和小程序 ID 两级隔离。   
支持内嵌 webview 内缓与小程序缓存隔离，获取内嵌 webview 指定 key 的缓存不会同时返回小程序相同 key 下的缓存数据。

## 使用限制
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验
![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/475b36a00434520a04d06c0d5a33d38e.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=none&width=127)

# 接口调用

## 示例

[小程序在线](https://opendocs.alipay.com/openbox/mini/opendocs/storage?view=preview&defaultPage=pages/index/index&defaultOpenedFiles=pages/index/index&theme=light) 

### .js 示例代码
```javascript
my.getStorage({
  key: 'currentCity',
  success: function(res) {
    my.alert({content: '获取成功：' + res.data});
  },
  fail: function(res){
    my.alert({content: res.errorMessage});
  }
});
```

## 入参

Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| key | String | 是 | 缓存数据的 key。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |


### Function success

success 回调函数会携带一个 Object 类型的对象，其属性如下：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| data | Object/String | key 对应的内容。 |


## 错误码



| **error** | **errorMessage** | **解决方案** |
| --- | --- | --- |
| 2 | 必填参数为空。 |  传入不为空的key。 | 



# 常见问题

## Q：缓存API存储的缓存什么情况下会被清除？
A：卸载支付宝客户端会清除缓存数据；长期未使用或在应用中心删除的小程序的缓存数据也会被系统清理。覆盖安装支付宝（不是先删除再安装）、支付宝设置中心清除缓存、关闭小程序，这三种操作不会导致小程序缓存失效。
 
## Q：如何主动清除缓存？
A：可以通过 [my.clearStorage](https://opendocs.alipay.com/mini/api/storage) 或 [my.clearStorageSync](https://opendocs.alipay.com/mini/api/ulv85u) 清除当前小程序下的本地数据缓存， 通过 [my.removeStorage](https://opendocs.alipay.com/mini/api/of9hze) 或 [my.removeStorageSync](https://opendocs.alipay.com/mini/api/ytfrk4) 移除指定 key 的本地缓存。

## Q：my.setStorage 接口存储的缓存有效期？
A：除非主动清除 或 卸载支付宝客户端，缓存数据会永久保存在本地。

## Q：插件和小程序的存储是否互通?
A：插件和小程序的缓存存储不通用，独立隔离。
