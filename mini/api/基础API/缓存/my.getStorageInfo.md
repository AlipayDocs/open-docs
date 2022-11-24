# 简介

**my.getStorageInfo** 是获取当前 storage 的相关信息的异步接口。

在内嵌的 webview 中，使用此 API 可以获取 webview 页面中的 storage 信息，但不会获取到当前小程序 storage 的相关信息。

## 使用限制

- 缓存数据本地加密存储，通过 API 读取时会自动解密返回。
- 覆盖安装支付宝（不是先删除再安装）、关闭小程序，这两种操作均不会导致小程序缓存失效。<br />开发者调用 API 存储的缓存数据，需要自行调用对应的删除/清除 API 进行删除。<br />长期未使用或在应用中心删除的小程序的缓存数据也会被系统清理。
- 小程序缓存默认具有支付宝账号和小程序 ID 两级隔离。
- iOS 客户端支持 iTunes 备份。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验

![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/c3268c2a3fa17b2d75125698a19b64fd.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=none&width=127)

# 接口调用

## 示例

[小程序在线](https://opendocs.alipay.com/openbox/mini/opendocs/storage?view=preview&defaultPage=pages/index/index&defaultOpenedFiles=pages/index/index&theme=light)

### .js 示例代码

```javascript
// .js
my.getStorageInfo({
  success: function (res) {
    console.log(res.keys);
    console.log(res.currentSize);
    console.log(res.limitSize);
  },
});
```

## 入参

Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

### Function success

success 回调函数会携带一个 Object 类型的对象，其属性如下：

| **属性**    | **类型**     | **描述**                        |
| ----------- | ------------ | ------------------------------- |
| keys        | String Array | 当前 storage 中所有的 key。     |
| currentSize | Number       | 当前占用的空间大小, 单位为 KB。 |
| limitSize   | Number       | 限制的空间大小，单位为 KB。     |
