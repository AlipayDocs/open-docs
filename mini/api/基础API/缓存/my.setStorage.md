# 简介

**my.setStorage** 是在本地存储数据的 API。

数据按 key 存储。单个 key 允许存储的数据最大为 200KB，单个小程序本地数据存储上限为 10MB。
数据存储时会被自动加密，相应的接口读取时也会自动解密，开发者通常无需另行加解密。

#### 数据隔离
+ 小程序本地数据按支付宝账号和小程序 ID 两个维度隔离：同一设备上，不同用户使用同一小程序数据不互通，同一用户使用的不同小程序在数据也不互通；
+ web-view 组件内页面用 my.setStorage/my.getStorage 存取的数据与包含它的小程序隔离；
+ 插件本地存储数据与宿主小程序隔离。

#### 数据清除
+ 用户卸载支付宝客户端，所有小程序本地数据会被一并清除；
+ 用户在我“我的小程序“中删除小程序，被删除的小程序本地数据会被清除；
+ 开发者可通过 [my.clearStorage](https://opendocs.alipay.com/mini/api/storage) 清除当前小程序的所有本地数据，或通过 [my.removeStorage](https://opendocs.alipay.com/mini/api/of9hze) 删除指定数据项。

**退出小程序或支付宝、在支付宝的设置界面清除缓存、覆盖安装（不是先删除再安装）支付宝**，这几种操作都不会清除小程序在本地存储的数据。

## 使用限制
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验
![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/2903725b254087040533640ca9de06a1.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=none&width=127)

# 接口调用

## 示例
[小程序在线](https://opendocs.alipay.com/openbox/mini/opendocs/storage?view=preview&defaultPage=pages/index/index&defaultOpenedFiles=pages/index/index&theme=light) 

### .js 示例代码
```javascript
my.setStorage({
  key: 'currentCity',
  data: {
    cityName: '杭州',
    adCode: '330100',
    spell: 'hangzhou',
  },
  success: res => {
    console.log("存储数据 success callback:", res);
    my.alert({ content: "写入成功" });
  },
  fail: err => {
    console.log("存储数据 fail callback:", err);
    my.alert({ content: "写入失败" });
  },
  complete: res => {
    console.log("存储数据 complete callback:", res);
  }
});
```

## 入参
Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| key | String | 是 | 存储数据的 key。不允许为空字符串。 |
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

## Q：如何更新存储的数据？
A：[my.setStorage](https://opendocs.alipay.com/mini/api/eocm6v) 传入相同的 key 即可覆盖已有数据。

## Q：小程序本地存储 setStorage 和 H5 本地存储 localStorage 有何差异？
A：H5 的 localStorage 只能存储 String，小程的 setStorage 支持 String，也支持 Object（内部会自动进行 JSON 序列化）。

## Q：小程序数据到达 10MB 后会继续写入数据会怎样?
A：超过 10MB 后无法继续写入，会触发 fail 回调（errorCode 12）。建议通过 [my.removeStorage](https://opendocs.alipay.com/mini/api/of9hze) 及时移除不再需要的数据。

