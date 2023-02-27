# 简介

**my.getStorageInfo** 是获取数据缓存相关信息的异步接口。

如需读取缓存数据本身，请使用 [my.getStorage](https://opendocs.alipay.com/mini/api/azfobl) 或 [my.getStorageSync](https://opendocs.alipay.com/mini/api/ox0wna) 。

## 扫码体验

![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/c3268c2a3fa17b2d75125698a19b64fd.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=none&width=127)

# 接口调用

## 示例

[小程序在线](https://opendocs.alipay.com/openbox/mini/opendocs/storage?view=preview&defaultPage=pages/index/index&defaultOpenedFiles=pages/index/index&theme=light)

### .js 示例代码

```javascript
my.getStorageInfo({
  success: function (res) {
    console.log(res.keys);
    console.log(res.currentSize);
    console.log(res.limitSize);
  },
  fail: function (err) {
   my.alert({ title: 'getStorageInfo 失败', content: JSON.stringify(err) });
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
| keys        | String Array | 本地缓存数据中所有的 key。     |
| currentSize | Number       | 已占用的空间大小，单位为 KB。 |
| limitSize   | Number       | 可用的总空间大小，单位为 KB。     |
