# 简介
**my.hideShareMenu** 是隐藏当前页面分享按钮的 API。

## 使用限制

- 基础库 [1.7.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端  10.1.10 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 调用此 API 后，分享按钮不会被隐藏，而是会被至灰，并显示 **当前页面不可分享**。<br />![hideshare XXX.png](https://cdn.nlark.com/yuque/0/2022/png/179989/1650877509568-ef7560f7-caef-4a24-ad62-a9ed600a6141.png#align=left&display=inline&height=258&margin=%5Bobject%20Object%5D&name=hideshare%20XXX.png&originHeight=928&originWidth=1080&size=93199&status=done&style=stroke&width=300)
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码
```javascript
// .js
my.hideShareMenu();
```

# 入参
入参为 Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |
