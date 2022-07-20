# 简介
**my.getAddress** 是获取用户收货地址的 API。

接口调用时会弹出用户已录入的收货地址列表供其选择，返回选中的项。如果用户尚未授权，会先弹出授权框，如果拒绝授权则触发 fail 回调。
已授权的用户，也可在小程序设置中撤销对当前小程序的”用户信息“授权。

## 使用限制

- 此 API 暂仅支持企业支付宝小程序使用。
- 基础库 [1.20.4](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.75 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 调用此 API 前需登录 [开放平台控制台](https://openhome.alipay.com/develop/manage) > 点击小程序，进入小程序详情页 > **开发** > **产品绑定** > **绑定产品**，选择绑定 **获取会员收货地址**。
- 根据《中华人民共和国个人信息保护法》，为进一步规范开发者的用户个人信息处理行为，保障用户合法权益，支付宝小程序无论是通过调用支付宝官方提供的涉及用户个人信息的相关接口，还是开发者自行收集用户个人信息，均需补充相应的小程序隐私政策。详情可查看 [小程序隐私政策](https://opendocs.alipay.com/mini/03lwro)。

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

用户通过授权并完成或取消选择，会触发 success 回调。success 回调将收到一个 Object 类型的参数，其属性如下：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| resultStatus | Number | 结果码。9000 表示用户选择了一个地址；6001 表示用户未做选择直接返回。 |
| result | Object \| "" | 结果详情。resultStatus 为 9000 时 result 为包含地址信息的对象（详见下文 <b>Object result</b>），resultStatus 为 6001 时，result 为空字符串。 

注意：当前 IDE 模拟器内的 my.getAddress 与真机上略有差异，用户授权但不选择直接返回时，不会有回调函数。

### Object result
用户选择的地址信息，包含以下属性：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| address | String | 详细地址。如 "浙江省杭州市西湖区西溪路556号" |
| country | String | 国家。如 "中国" | 
| prov | String | 省。如 "浙江省" | 
| city | String | 市。如 "杭州市" | 
| area | String | 区。如 "西湖区" | 
| street | String | 街道。如 "古荡街道" | 
| fullname | String | 名称。如 "张三" | 
| mobilePhone | String | 手机号。如 "18100000000" |

## fail 回调

用户拒绝授权发生其他异常，会触发 fail 回调，收到的参数对象包含 error(错误码） 和 errorMessage（错误消息） 属性。

| **错误码** | **错误消息** | **解决方案** |
| --- | --- | --- |
| 4 | 无权限调用该接口。 | 下次调用 my.getAddress 时，仍会弹出授权框，如果用户同意授权，则会进入 success 回调 |

# 常见问题 FAQ

## Q：my.getAddress 每次都会弹授权提示框吗？授权有效期是多久？
A：如果用户没有授权，每次调用都会弹出授权提示；如果已经授权，则不会再弹，直到用户通过小程序设置撤销了“用户信息”授权。

## Q：my.getAddress 能否返回省市区编码？
A：暂未提供此能力。需要开发者自己用名称匹配。
