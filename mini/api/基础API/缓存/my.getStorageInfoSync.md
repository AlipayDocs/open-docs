
# 简介
**my.getStorageInfoSync** 是获取当前 storage 相关信息的同步接口。

## 使用限制

- 缓存数据本地加密存储，通过 API 读取时会自动解密返回。
- 覆盖安装支付宝（不是先删除再安装），不会导致小程序缓存失效。
- 支付宝设置中心清除缓存不会导致小程序缓存失效。
- 小程序缓存默认具有支付宝账号和小程序 ID 两级隔离。
- iOS 客户端支持 iTunes 备份。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验
![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/4f05973521afe7c35c64f84c2fd19ea8.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=none&width=127)

# 接口调用

## Herbox
[小程序在线](https://herbox-embed.alipay.com/s/doc-storage?&chInfo=openhome-doc) 

## 示例代码

### .js 示例代码
```javascript
// .js
var res = my.getStorageInfoSync()
console.log(res.keys)
console.log(res.currentSize)
console.log(res.limitSize)
```

## 返回值
| **属性** | **类型** | **描述** |
| --- | --- | --- |
| keys | String/Array | 当前 storage 中所有的 key。 |
| currentSize | Number | 当前占用的空间大小, 单位为 KB。 |
| limitSize | Number | 限制的空间大小，单位为 KB。 |

