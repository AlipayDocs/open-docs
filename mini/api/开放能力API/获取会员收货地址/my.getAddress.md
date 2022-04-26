# 简介
**my.getAddress** 是商家在寄送外卖、快递或其它场景需要用户填写地址信息时，可通过调用此 API 直接获取地址数据，无需用户手动填写。详情可查看 [获取会员收货地址](https://opendocs.alipay.com/mini/introduce/getaddress) 能力介绍。

调用接口时会弹出授权框，用户点击弹框按钮同意授权后，可以通过接口获取到返回的收货地址数据。若用户未授权，则无法返回正确信息。

## 使用限制

- 基础库 [1.20.4](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.75 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 由于开发者工具版本限制，目前 my.getAddress 接口暂不支持在开发者工具调试和真机调试，仅支持真机预览。开发者请调至 **预览** 模式，在支付宝客户端扫码查看效果。
- 此 API 暂仅支持企业支付宝小程序使用。
- 因该 JSAPI 涉及获取用户隐私信息，使用该 JSAPI 前，请对照以下文档检查应用是否符合主营行业及字段使用场景的要求：[用户信息申请及使用基础规则](https://opendocs.alipay.com/mini/introduce/01sxqf)。

# 接口调用

## 示例代码

### .js 示例代码
```javascript
// .js
my.getAddress({
  success: (res) => {
    my.alert({
      title: JSON.stringify(res)
    });
  }
});
```

## 返回示例

#### 正常响应
```json
// 正常响应
{
  "resultStatus": "9000",
  "result": {
    "address": "浙江省杭州市西湖区西溪路556号", // 详细地址
    "country": "中国", // 国家名称
    "prov": "浙江省", // 省
    "city": "杭州市", // 市
    "area": "西湖区", // 区
    "street": "", // 街道
    "fullname": "张三", // 名称
    "mobilePhone": "182XXXXXXX" // 手机号
  }
}
```

#### 服务端接口异常响应
```json
// 用户取消操作响应
{ 
  "result": '',
  "resultStatus": '6001'
}
// 用户拒绝授权响应
{
  "error": 4,
  "errorMessage": "无权调用该接口"
}
```

## 入参
Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| success | Function | 否 | 接口调用成功的回调函数。 |
| fail | Function | 否 | 接口调用失败的回调函数。 |
| complete | Function | 否 | 接口调用结束的回调函数（调用成功、失败都会执行）。 |

## Function success

success 回调函数会携带一个 Object 类型的对象，其属性如下：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| address | String | 详细地址。 |
| country | String | 国家名称。 |
| prov | String | 省。 |
| city | String | 市。 |
| area | String | 区。 |
| street | String | 街道。 |
| fullname | String | 用户名。 |
| mobilePhone | String | 手机号。 |
