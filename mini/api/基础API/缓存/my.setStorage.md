# 简介
**my.setStorage** 是将数据存储在本地缓存中指定的 key 中的异步接口，会覆盖掉原来该 key 对应的数据。

支持内嵌 webview 的存储与小程序存储隔离，内嵌 webview 中指定 key 存储数据不会覆盖小程序自身相同 key 对应的数据。

## 使用限制

- 单个 key 允许存储的最大数据大小为 200KB，所有数据存储上限为 10MB。
- 缓存数据本地加密存储，通过 API 读取时会自动解密返回。
- 覆盖安装支付宝（不是先删除再安装）、关闭小程序，这两种操作均不会导致小程序缓存失效。<br />开发者调用 API 存储的缓存数据，需要自行调用对应的删除/清除 API 进行删除。<br />长期未使用或在应用中心删除的小程序的缓存数据也会被系统清理。
- 小程序缓存默认具有支付宝账号和小程序 ID 两级隔离。
- iOS 客户端支持 iTunes 备份。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验
![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/2903725b254087040533640ca9de06a1.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=none&width=127)

# 接口调用

## 示例
[小程序在线](https://opendocs.alipay.com/examples/e4f97280-1e31-4262-a4ee-498a786dd4a0) 

### .js 示例代码
```javascript
// .js
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

