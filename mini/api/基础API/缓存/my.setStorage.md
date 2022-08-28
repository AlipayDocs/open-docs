# 简介

**my.setStorage** 将数据存储在本地缓存中指定的 key 中。该 key 原来对应的内容会被覆盖。除非用户主动删除或因存储空间原因被系统清理，否则数据都一直可用。单个 key 允许存储的最大数据长度为 200KB，所有数据存储上限为 10MB。

**相关接口**
+ 本地缓存数据使用 my.setStorage 按 key 存储，使用 my.getStorage 按 key 读取；
+ 可使用 my.getStorageInfo 获取已存储的所有 key 以及总体空间占用情况；
+ 可使用 my.removeStorage 删除指定 key 对应数据，使用 my.clearStorage 删除所有缓存数据；
+ 本地缓存数据相关的 API 均提供带 Sync 后缀的同步版本，但通常推荐使用异步版本，以免影响页面加载和交互响应速度。

**数据隔离**
+ 本地缓存数据按支付宝账号和小程序 appId 两个维度隔离：同一设备上，不同账号的数据互相隔离，同一账号在不同小程序里的数据互相隔离；
+ web-view 组件内页面用 my.setStorage/my.getStorage 存取的数据与包含它的小程序隔离；
+ 插件本地缓存数据与宿主小程序隔离。

**数据清除**
+ 用户卸载支付宝客户端，所有小程序本地缓存数据会被一并清除；
+ 用户在我“我的小程序”中删除小程序，被删除小程序的本地缓存数据会被清除；
+ **不会**清除数据的情况：退出小程序或支付宝、在支付宝的设置界面清除缓存、覆盖安装（不是先删除再安装）支付宝。


# 接口调用

## 示例代码

```javascript
my.setStorage({
  key: 'currentCity',
  data: {
    cityName: '杭州',
    adCode: '330100',
    spell: 'hangzhou',
  },
  success: (res) => {
    my.alert({ title: "setStorage success" });
  },
  fail: (err) => {
    my.alert({ title: "setStorage success", content: JSON.stringify(err) });
  },
});
```

## 入参

Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| key | String | 是 | 存储数据的 key。不接受空字符串。 |
| data | Object/String | 是 | 要存储的数据。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

## 错误码

| **error** | **errorMessage** | **解决方案** |
| --- | --- | --- |
| 2 | 必填参数为空  |  请检查必填参数是否填写。 | 
| 12 | 存储总大小达到上限 | 单个小程序数据存储上限为 10MB。可以通过 [my.removeStorage](https://opendocs.alipay.com/mini/api/of9hze) 及时移除不再需要的数据。| 
| 14 | data长度超限 | 单个 key 允许存储的最大数据大小为 200KB，可以减少 data 长度或拆分成多个 key 进行存储。| 

# 常见问题

## Q：支付宝小程序里 my.setStorage 是否支持 encrypt 入参？
A：支付宝小程序的本地缓存数据默认加密存储，不支持/不需要 encrypt 参数。

## Q：小程序数据到达 10MB 后会继续写入数据会怎样?
A：超过 10MB 后无法继续写入，会触发 fail 回调（错误码 12）。建议通过 [my.removeStorage](https://opendocs.alipay.com/mini/api/of9hze) 及时移除不再需要的数据。

## Q：小程序的 my.setStorage 和 H5 本地存储 localStorage 有何差异？
A：H5 的 localStorage 只能存储 String，小程的 my.setStorage 支持 String，也支持 Object（内部会自动做 JSON 序列化）。

## Q：web-view 组件里 H5 是否可以调用 my.setStorage？
A：在 web-view 组件里 H5 引入 https://appx/web-view.min.js 后，可以调用 my.setStorage/my.getStorage，但请注意，它们操作的是 web-view 内的数据，与小程序数据并不相通。web-view 里想要利用小程序的数据，必须通过 [my.postMessage/my.onMessage](https://opendocs.alipay.com/mini/component/web-view#%E7%A4%BA%E4%BE%8B%E4%BB%A3%E7%A0%81_2) 与小程序通信。
