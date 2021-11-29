
# 简介
**my.ap.updateAlipayClient** 是用于打开支付宝客户端升级界面的 API，用户可主动选择升级支付宝客户端。

## 使用限制

- 基础库 [1.10.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.32 或更高版本，若版本较低，建议采取 [兼容处理](/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码
```javascript
// .js
my.ap.updateAlipayClient({
  success: () => {
    my.alert({
      title: '升级成功',
    });
  },
  fail: () => {
    my.alert({
      title: '升级失败',
    });
  },
});
```

## 入参
Object 类型，属性如下：

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |


### success 回调函数
入参为 Object 类型，属性如下：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| success | Boolean | 跳转成功。 |


### fail 回调函数
入参为 Object 类型，属性如下：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| error | String | 错误码。 |
| errorMessage | String | 错误信息。 |


## 错误码
| **错误码** | **说明** |
| --- | --- |
| 3 | 发生未知错误。 |

