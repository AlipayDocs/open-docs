# 简介

**my.getStorage** 从本地缓存中异步获取指定 key 的内容。


# 接口调用

## 示例代码

```javascript
my.getStorage({
  key: 'currentCity',
  success: (res) => {
    my.alert({ title: 'getStorage success', content: JSON.stringify(res.data) });
  },
  fail: (err) => {
    my.alert({ title: "setStorage fail", content: JSON.stringify(err) });
  },
});
```

## 入参

Object 类型，属性如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| key | String | 是 | 要读取数据的 key。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

### Function success

success 回调函数会携带一个 Object 类型的对象，其属性如下：

| **属性** | **类型**      | **描述**         |
| -------- | ------------- | ---------------- |
| data     | Object/String | key 对应的内容。 |

## 错误码

success 回调函数会携带一个 Object 类型的对象，包含 error 和 errorMessage 字段：

| **error** | **errorMessage** | **解决方案** |
| --- | --- | --- |
| 2 | 必填参数为空。 |  传入不为空的key。 | 

# 常见问题

## Q：web-view 组件里 H5 是否可以调用 my.getStorage？
A：在 web-view 组件里 H5 引入 https://appx/web-view.min.js 后，可以调用 my.setStorage/my.getStorage，但请注意，它们操作的是 web-view 内的数据，与小程序数据并不相通。web-view 里想要利用小程序的本地数据，必须通过 [my.postMessage/my.onMessage](https://opendocs.alipay.com/mini/component/web-view#%E7%A4%BA%E4%BE%8B%E4%BB%A3%E7%A0%81_2) 与小程序通信，由小程序代码调用实际调用 API
