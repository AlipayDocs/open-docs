# 简介

**my.getStorageInfo** 是获取当前 storage 的相关信息的异步接口。

**数据隔离**
+ 本地缓存数据按支付宝账号和小程序 appId 两个维度隔离：同一设备上，不同账号的数据互相隔离，同一账号在不同小程序里的数据互相隔离；
+ web-view 组件内页面用 my.getStorageInfo 取的数据与包含它的小程序隔离；
+ 插件本地缓存数据与宿主小程序隔离。

**数据清除**
+ 可使用 my.removeStorage 删除指定 key 对应数据，使用 my.clearStorage 删除所有缓存数据；
+ 用户卸载支付宝客户端，所有小程序本地缓存数据会被一并清除；
+ 用户在我“我的小程序”中删除小程序，被删除小程序的本地缓存数据会被清除；
+ **不会**清除数据的情况：退出小程序或支付宝、在支付宝的设置界面清除缓存、覆盖安装（不是先删除再安装）支付宝。

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
  fail: function (err) {
    console.log(err);
  },
  complete: function (res) {
    console.log(res);
  }
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
