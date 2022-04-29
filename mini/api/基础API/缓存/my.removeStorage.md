
# 简介
**my.removeStorage** 是删除缓存数据的异步接口。

移除内嵌 webview 的存储数据时不会移除当前小程序的存储数据。

## 使用限制

- 缓存数据本地加密存储，通过 API 读取时会自动解密返回。
- 覆盖安装支付宝（不是先删除再安装），不会导致小程序缓存失效。
- 支付宝设置中心清除缓存不会导致小程序缓存失效。
- 小程序缓存默认具有支付宝账号和小程序 ID 两级隔离。
- iOS 客户端支持 iTunes 备份。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验
![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/db1966f15bfc0949bfec677c98b00248.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=none&width=127)

# 接口调用

## 示例
[小程序在线](https://opendocs.alipay.com/examples/e4f97280-1e31-4262-a4ee-498a786dd4a0) 

### .js 示例代码
```javascript
// .js
my.removeStorage({
  key: 'currentCity',
  success: function(){
    my.alert({content: '删除成功'});
  }
});
```

## 入参
Object 类型，属性如下：

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| key | String | 是 | 缓存数据的 key。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

