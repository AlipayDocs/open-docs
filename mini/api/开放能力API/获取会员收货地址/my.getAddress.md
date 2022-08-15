# 简介
**my.getAddress** 是获取用户收货地址的 API。

接口调用时会弹出用户已录入的收货地址列表供其选择，返回选中的项。如果用户尚未授权，会先弹出授权框，如果拒绝授权则触发 fail 回调。
已授权的用户，也可在小程序设置中撤销对当前小程序的”用户信息“授权。

## 使用限制

- 此 API 暂仅支持企业支付宝小程序使用。
- 基础库 [1.20.4](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.75 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。

# 接口调用

## 示例代码

### .js 示例代码
```javascript
my.getAddress({
  success: (res) => {
   if (res.resultStatus == 9000) {
    my.alert({
      title: "getAddress success",
      content: JSON.stringify(res.result)
    });
   } else {
     console.log("getAddress cancel", JSON.stringify(res));
   }
  },
  fail: (res) => {
    my.alert({
      title: "getAddress fail",
      content: JSON.stringify(res)
    });
  }
});
```

## 入参

Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| success | Function | 否 | 接口调用成功的回调函数。 |
| fail | Function | 否 | 接口调用失败的回调函数。 |
| complete | Function | 否 | 接口调用结束的回调函数（调用成功、失败都会执行）。 |

## success 回调

已经授权的用户，完成或取消地址选择，都会触发 success 回调。success 回调将收到一个 Object 类型的参数，其属性如下：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| resultStatus | Number | 结果码。9000 表示用户选择了一个地址；6001 表示用户未做选择直接返回。 |
| result | Object \| "" | 结果详情。resultStatus 为 9000 时 result 为包含地址信息的对象（详见下文 <b>Object result</b>），resultStatus 为 6001 时，result 为空字符串。 

注意：当前 IDE 模拟器内的 my.getAddress 与真机略有差异，用户已授权但不选择（直接返回）时，不会触发回调函数。

### Object result

用户选择的地址信息，包含以下属性：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| address | String | 详细地址。如 "浙江省杭州市西湖区西溪路556号" |
| country | String | 国家。如 "中国" | 
| prov | String | 省。如 "浙江省" | 
| city | String | 市。如 "杭州市" | 
| area | String | 区。如 "西湖区" | 
| street | String | 街道。如 "古荡街道"。<br> **注意** ：因为历史遗留问题，目前此参数真机上返回为空。 | 
| fullname | String | 名称。如 "张三" | 
| mobilePhone | String | 手机号。如 "18100000000" |

## fail 回调

用户拒绝授权或发生其他异常，会触发 fail 回调，收到的参数对象包含 error（错误码）和 errorMessage（错误消息）属性。

| **错误码** | **错误消息** | **解决方案** |
| --- | --- | --- |
| 4 | 无权限调用该接口。 | 报错是因为用户在弹出的授权框中选择了拒绝。下次调用 my.getAddress 时授权框仍会弹出，用户同意授权即可进入 success 回调。 |

# 常见问题 FAQ

## Q：my.getAddress 每次都会弹授权提示框吗？授权有效期是多久？
A：如果用户没有授权，每次调用都会弹出授权提示；如果已经授权，则不会再弹，直到用户通过小程序设置撤销了“用户信息”授权。

## Q：my.getAddress 能否返回省市区编码？
A：未提供此能力，需要开发者自己用名称匹配。
