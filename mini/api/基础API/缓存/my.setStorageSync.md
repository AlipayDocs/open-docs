# 简介
**my.setStorageSync** 是将数据存储在本地缓存中指定的 key 中的同步接口。

## 使用限制

- 缓存数据本地加密存储，通过 API 读取时会自动解密返回。
- 覆盖安装支付宝（不是先删除再安装）、关闭小程序，这两种操作均不会导致小程序缓存失效。<br />开发者调用 API 存储的缓存数据，需要自行调用对应的删除/清除 API 进行删除。<br />长期未使用或在应用中心删除的小程序的缓存数据也会被系统清理。
- 小程序缓存默认具有支付宝账号和小程序 ID 两级隔离。
- iOS 客户端支持 iTunes 备份。
- 单个 key 允许存储的最大数据大小为 200KB，单个小程序的缓存总上限为 10MB（IDE 模拟器测试无限制）。
- 同步方法会阻塞当前任务，直到同步方法处理返回。
- 异步方法不会阻塞当前任务。
- 支持 **内嵌** webview 内缓与小程序缓存隔离，获取内嵌 webview 指定 key 的缓存不会同时返回小程序相同 key 下的缓存数据。
- 调用 API 清空内嵌 webview 的存储时不会同时清空当前小程序本身的存储数据。
- 调用 API 将数据存储在本地缓存中指定的 key 中，会覆盖掉原来该 key 对应的数据。由于内嵌 webview 的存储与小程序存储隔离，内嵌 webview 中指定 key 存储数据不会覆盖小程序自身相同 key 对应的数据。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验

![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/075fe99f9a07d6c7c312b806239c727f.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=none&width=127)

# 接口调用

## Herbox

[小程序在线](https://herbox-embed.alipay.com/s/doc-storage?&chInfo=openhome-doc) 

## 示例代码

### .js 示例代码

```javascript
// .js
my.setStorageSync({
  key: 'currentCity',
  data: {
    cityName: '杭州',
    adCode: '330100',
    spell: ' hangzhou',
  }
});
```

## 入参

Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| key | String | 是 | 缓存数据的 key。 |
| data | Object/String | 是 | 要缓存的数据。 |
