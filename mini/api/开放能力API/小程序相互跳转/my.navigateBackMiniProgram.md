# 简介
**my.navigateBackMiniProgram** 是用于跳转回上一个小程序的 API，只有当另一个小程序跳转到当前小程序时才能调用成功。

相关问题可查看 [小程序相互跳转 FAQ](https://opendocs.alipay.com/mini/api/xqvxl4)。

## 使用限制

此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码
```javascript
// .js
my.navigateBackMiniProgram({
	extraData:{
  	   "data1":"test"
    },
	success: (res) => {
	   console.log(JSON.stringify(res))
    },
    fail: (res) => {
	   console.log(JSON.stringify(res))
    }
});
```

## 入参
Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| extraData | Object | 否 | 需要传递给目标小程序的数据，目标小程序可在 App.onLaunch()、App.onShow() 中获取到这份数据。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

