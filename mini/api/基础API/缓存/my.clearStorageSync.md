# 简介

**my.clearStorageSync** 是清除本地数据缓存的同步接口。

小程序缓存默认具有支付宝账号和小程序 ID 两级隔离。
内嵌 webview 的缓存数据与小程序缓存数据相互隔离，即清理内嵌 webview 中缓存数据时不会清理小程序自身的缓存数据。

## 扫码体验

![|127x157](https://gw.alipayobjects.com/os/skylark-tools/public/files/d4f26e73f7bae3f561da63e179c8060a.jpeg%26originHeight%3D157%26originWidth%3D127%26size%3D19905%26status%3Ddone%26width%3D127#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=none&width=127)

# 接口调用

## 示例

[小程序在线](https://opendocs.alipay.com/openbox/mini/opendocs/storage?view=preview&defaultPage=pages/index/index&defaultOpenedFiles=pages/index/index&theme=light)

### .js 示例代码

```javascript
// .js
my.clearStorageSync();
```
