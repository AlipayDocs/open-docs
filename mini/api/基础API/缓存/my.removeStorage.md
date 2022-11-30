# 简介

**my.removeStorage** 是删除指定 key 对应的缓存数据的异步接口。

小程序缓存默认具有支付宝账号和小程序 ID 两级隔离。     
内嵌 webview 的缓存数据与小程序缓存数据相互隔离。删除内嵌 webview 中指定 key 对应的缓存数据时，小程序自身的缓存数据并不会被删除。

## 扫码体验

![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/db1966f15bfc0949bfec677c98b00248.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=none&width=127)

# 接口调用

## 示例

[小程序在线](https://opendocs.alipay.com/openbox/mini/opendocs/storage?view=preview&defaultPage=pages/index/index&defaultOpenedFiles=pages/index/index&theme=light)

### .js 示例代码

```javascript
// .js
my.removeStorage({
  key: 'currentCity',
  success: function () {
    my.alert({ content: '删除成功' });
  },
  fail: function () {
    my.alert({ content: '删除失败' });
  },
  complete: function () {
    my.alert({ content: '调用结束' });
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
