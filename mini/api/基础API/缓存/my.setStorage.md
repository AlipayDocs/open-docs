# 简介

**my.setStorage** 是将数据存储在指定的 key 的本地缓存中的异步接口，会覆盖掉原来该 key 对应的数据。


缓存本地数据时会自动加密存储，通过 API 读取时会自动解密返回。   
小程序缓存默认具有支付宝账号和小程序 ID 两级隔离。   
内嵌 webview 的存储与小程序存储相互隔离，即内嵌 webview 中指定 key 存储数据不会覆盖小程序自身相同 key 对应的数据。

## 使用限制
- 单个 key 允许存储的最大数据大小为 200KB，单个小程序数据存储上限为 10MB。
- iOS 客户端支持 iTunes 备份。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验
![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/2903725b254087040533640ca9de06a1.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=none&width=127)

# 接口调用

## 示例
[小程序在线](https://opendocs.alipay.com/openbox/mini/opendocs/storage?view=preview&defaultPage=pages/index/index&defaultOpenedFiles=pages/index/index&theme=light) 

### .js 示例代码
```javascript
my.setStorage({
  key: 'currentCity',
  data: {
    cityName: '杭州',
    adCode: '330100',
    spell: ' hangzhou',
  },
  success: function() {
    my.alert({content: '写入成功'});
  }
});
```

## 入参
Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| key | String | 是 | 缓存数据的 key。 |
| data | Object/String | 是 | 要缓存的数据。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |


## 错误码



| **error** | **errorMessage** | **解决方案** |
| --- | --- | --- |
| 11 | invalid params | 无效的传参，请检查传参是否规范。| 
| 12 | 存储总大小达到上限 | 单个小程序数据存储上限为 10MB。可以通过 [my.removeStorage](https://opendocs.alipay.com/mini/api/of9hze) 或 [my.removeStorageSync](https://opendocs.alipay.com/mini/api/ytfrk4) 及时移除不必要的存储。| 
| 14 | data 长度超限 | 单个 key 允许存储的最大数据大小为 200KB，可以减少 data 长度或拆分成多个 key 进行存储。| 



# 常见问题

## Q：缓存 API 存储的缓存什么情况下会被清除？
A：卸载支付宝客户端会清除缓存数据；长期未使用或在应用中心删除的小程序的缓存数据也会被系统清理。覆盖安装支付宝（不是先删除再安装）、支付宝设置中心清除缓存、关闭小程序，这三种操作不会导致小程序缓存失效。
 
## Q：如何主动清除缓存？
A：可以通过 [my.clearStorage](https://opendocs.alipay.com/mini/api/storage) 或 [my.clearStorageSync](https://opendocs.alipay.com/mini/api/ulv85u) 清除当前小程序下的本地数据缓存， 通过 [my.removeStorage](https://opendocs.alipay.com/mini/api/of9hze) 或 [my.removeStorageSync](https://opendocs.alipay.com/mini/api/ytfrk4) 移除指定 key 的本地缓存。

## Q：my.setStorage 接口存储的缓存有效期？
A：除非主动清除 或 卸载支付宝客户端，缓存数据会永久保存在本地。

## Q：如何更新小程序缓存？
A：可以使用 [my.setStorage](https://opendocs.alipay.com/mini/api/eocm6v) 或 [my.setStorageSync](https://opendocs.alipay.com/mini/api/cog0du) 存入相同的 key 即可覆盖之前的缓存。

## Q：小程序本地存储 setStorage 和 h5 本地存储 localStorage 的区别。
A：h5 本地存储 localStorage 在做数据存储的时候，只能存储 String 类型的值。当存储的值需要为 Object 类型时，需要在读和写的时候都做一步特殊处理。
  小程序本地存储支持 String 和 Object 两种数据类型的存储。

## Q：插件和小程序的存储是否互通?
A：插件和小程序的缓存存储不通用，独立隔离。

## Q：小程序缓存到达 10MB 后会清除之前的数据再写入还是写入报错?
A：当超过 10MB 会无法继续写入，并提示：error 12，data 长度超限。可以通过 [my.removeStorage](https://opendocs.alipay.com/mini/api/of9hze) 或 [my.removeStorageSync](https://opendocs.alipay.com/mini/api/ytfrk4) 及时移除不必要的存储。

