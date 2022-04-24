# 简介
**my.getStorageSync** 是获取缓存数据的同步接口。

## 使用限制

- 缓存数据本地加密存储，通过 API 读取时会自动解密返回。
- 覆盖安装支付宝（不是先删除再安装）、关闭小程序，这两种操作均不会导致小程序缓存失效。<br />开发者调用 API 存储的缓存数据，需要自行调用对应的删除/清除 API 进行删除。<br />长期未使用或在应用中心删除的小程序的缓存数据也会被系统清理。
- 小程序缓存默认具有支付宝账号和小程序 ID 两级隔离。
- iOS 客户端支持 iTunes 备份。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验
![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/ba4bc193ccca7852332a6b37005e0bdc.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=none&width=127)

# 接口调用

## Herbox
[小程序在线](https://herbox-embed.alipay.com/s/doc-storage?&chInfo=openhome-doc) 

## 示例代码

### .js 示例代码
```javascript
// .js
let res = my.getStorageSync({ key: 'currentCity' });
 my.alert({
    content: JSON.stringify(res.data),
 });
```

## 入参

Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| key | String | 是 | 缓存数据的 key。 |


## 返回值

返回一个 Object 类型的对象，其属性如下：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| data | Object/String | key 对应的内容。 |

