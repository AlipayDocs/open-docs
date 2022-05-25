# 简介

**my.redirectTo** 是关闭当前页面，跳转到应用内的某个指定页面的 API。

相关问题可查看 [路由FAQ](https://opendocs.alipay.com/mini/api/fu8l65) 。

## 使用限制

此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验

![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/da4e4eadc547ca2cfd6476ccf706db38.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=none&width=127)

# 接口调用

## 示例

### .js 示例代码
```javascript
// .js
my.redirectTo({
  url: 'new_page?count=100' //路径可以使用相对路径或绝对路径的方式进行传递
})
```
以跳转至首页 index 页面为例：

- 使用绝对路径：`url: /pages/index/index`。
- 使用相对路径：`url: ../index/index`。

## 入参

Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| url | String | 是 | 需要跳转的应用内非 tabbar 的目标页面路径 ,路径后可以带参数。带参数时请参考[小程序全局 / 页面参数设置以及解析细节](https://opendocs.alipay.com/mini/03durs) |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

