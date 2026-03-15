# 简介

**my.tradePay** 是用于发起支付的 API。使用该能力需要前往小程序控制台签约**当面付**能力才可使用。

## 使用限制

此 API 暂仅支持企业支付宝小程序使用。

# 接口调用

## 示例代码

#### 小程序支付

```javascript
// .js
my.tradePay({
  // 调用统一收单交易创建接口（alipay.trade.create），获得返回字段支付宝交易号trade_no
  tradeNO: '201711152100110410533667792',
  success: res => {
    my.alert({
      content: JSON.stringify(res),
    });
  },
  fail: res => {
    my.alert({
      content: JSON.stringify(res),
    });
  },
});
```

#### 支付宝预授权

```javascript
// .js
my.tradePay({
  // 调用资金冻结接口（alipay.fund.auth.order.app.freeze），获取支付宝预授权参数
  orderStr:
    'alipay_sdk=alipay-sdk-java-3.0.118.DEV&app_id=2018112803019836&biz_content=%7B%22amount%22%3A%220.02%22%2C%22extra_param%22%3A%22%7B%5C%22category%5C%22%3A%5C%22CHARGE_PILE_CAR%5C%22%7D%22%2C%22order_title%22%3A%22%D6%A7%B8%B6%B1%A6%D4%A4%CA%DA%C8%A8%22%2C%22out_order_no%22%3A%22ZMOutOrderNoAppFreeze2018052915543415090975%22%2C%22out_request_no%22%3A%22ZMOutReqNoAppFreeze20180529155434581875858%22%2C%22pay_timeout%22%3A%222d%22%2C%22payee_user_id%22%3A%222088202224929664%22%2C%22product_code%22%3A%22PRE_AUTH_ONLINE%22%7D&charset=GBK&format=json&method=alipay.fund.auth.order.app.freeze&sign=L4wk%2FNKcbJOo3n6Q5qbPzn0jUsvZlK4jr7iXnghudR0zeWJMmeNC71qIBSQfIz45n%2B5iTd0NQ5IK581xI2xCShTCiKAywnQcDmA%2Bjf%2BrRdKCDQCMLfCz%2BZ37C%2B6zxAX3e81%2F8Hr29lw4VPFfHkp9FmMwKw%2FGkNfV5ZlWoh7UtN8%3D&sign_type=RSA&timestamp=2018-05-29+15%3A54%3A35&version=1.0',
  success: res => {
    my.alert({
      content: JSON.stringify(res),
    });
  },
  fail: res => {
    my.alert({
      content: JSON.stringify(res),
    });
  },
});
```

## 入参

Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| tradeNO | String | 否（调用 [小程序支付](https://opendocs.alipay.com/mini/introduce/pay) 时必填） | 接入小程序支付时传入此参数。此参数为支付宝交易号，注意参数有大小写区分。 |
| orderStr | String | 否（调用 [支付宝预授权](https://opendocs.alipay.com/mini/introduce/pre-authorization) 时必填） | 完整的支付参数拼接成的字符串，从服务端获取。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

### Function success

success 回调函数会携带一个 Object 类型的对象，其属性如下：

| **属性**   | **类型** | **描述**               |
| ---------- | -------- | ---------------------- |
| resultCode | String   | 支付结果码，详见下表。 |

#### 结果码

| **结果码** | **描述** | **解决方案** |
| --- | --- | --- |
| 4 | 无权限调用（N22104）。 | 个人小程序应用没有开放小程序支付能力。 |
| 9000 | 订单处理成功。 | 不建议根据 my.tradePay 接口同步返回判断是否支付成功，9000 不能判定就是支付成功，请以异步通知（notify_url）返回的 trade_status(交易状态)为 TRADE_SUCCESS + [alipay.trade.query](https://opendocs.alipay.com/mini/02j2c2)（统一收单线下交易查询接口）查询订单是否支付成功实际返回的支付状态为准。 |
| 8000 | 正在处理中。支付结果未知（有可能已经支付成功）。 | 请调用 [alipay.trade.query](https://opendocs.alipay.com/mini/02j2c2)（统一收单线下交易查询接口）查询商户订单列表中订单的支付状态，以查询接口实际返回的支付状态为准。 |
| 4000 | 订单处理失败。 | tradeNO 调用 [小程序支付](https://opendocs.alipay.com/mini/introduce/pay) 时必填，orderStr 调用 [支付宝预授权](https://opendocs.alipay.com/mini/introduce/pre-authorization) 时必填，二选一。根据具体接入开放能力选择参数。<br />**小程序支付时：**<ul><li>检查入参字段 tradeNO 是否编写正确，"NO"都是大写。</li><li>tradeNO 的入参数据是 [alipay.trade.create](https://opendocs.alipay.com/mini/02j1c4)（统一收单交易创建接口）返回的 “trade_no”，不是 “out_trade_no”。</li></ul>**支付宝预授权时：**<ul><li>orderStr 必填。</li><li>[alipay.fund.auth.order.app.freeze](https://opendocs.alipay.com/mini/02f0g0)（线上资金授权冻结接口）的参数有误，导致通过 response.sdkExcute(request) 方法获取到的 orderStr 参数有问题，检查入参字段和数据是否符合接口要求，建议只传必传参数测试，避免其它参数干扰。</li></ul> |
| 6001 | 用户中途取消。 | <ul><li>请用户重新签约 / 支付。</li><li>检查 tradeNO 的入参是否为正常入参，参数数据为 [alipay.trade.create](https://opendocs.alipay.com/mini/02j1c4)（统一收单交易创建接口）返回的“trade_no”。</li><li><b>alipay.trade.create</b>（统一收单交易创建接口）在小程序场景中 <b>buyer_id</b> 参数必填，且入参的 <b>buyer_id</b>（用户 user_id，2088 开头）必须和前端唤起支付的支付宝账号一致。</li></ul> |
| 6002 | 网络连接出错。 | 检查网络连接后重试。 |
| 6004 | 处理结果未知（有可能已经成功）。 | 请调用 [alipay.trade.query](https://opendocs.alipay.com/mini/02j2c2)（统一收单线下交易查询接口）查询商户订单列表中订单的支付状态，以查询接口实际返回的支付状态为准。 |

# 常见问题 FAQ

## Q：web-view 中如何进行支付？

A：web-view 中也可以通过 my.tradePay API 进行支付，不支持 H5 网页支付。

## Q：小程序唤起支付可以支付其它 APPID 或者 PID 的订单吗？

A：小程序 my.tradePay 接口不会限制创建 tradeNO 交易号参数的应用 APPID，只要交易号合法即可。

## Q：小程序唤起支付提示ISV权限不足？

A：需要登录小程序后台签约[当面付](https://opendocs.alipay.com/open/194/105072)能力.

更多问题可查看 [小程序支付 / 支付宝预授权 FAQ](https://opendocs.alipay.com/mini/api/tmz0kq) 。
