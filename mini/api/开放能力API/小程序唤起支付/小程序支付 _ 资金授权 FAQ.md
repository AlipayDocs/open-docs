### Q：支付宝预授权场景下，在 IDE 上调用 my.tradePay 报错 “error 2:无效 API 入参”，如何处理？

A：IDE 模拟器调用 my.tradePay 后会生成一个支付二维码（有效时间 10 分钟），开发者在支付宝客户端扫码支付，支付结果会同步 my.tradePay 回调。

![](http://mdn.alipayobjects.com/afts/img/A*G8e2RJF3OYQAAAAAAAAAAABkAa8wAA/1024w_1024h_1l.png?bz=openpt_doc&t=1CYtMLzOixg-Jl8Zof84yQAAAABkMK8AAAAA#align=left&display=inline&height=345&margin=%5Bobject%20Object%5D&originHeight=345&originWidth=854&status=done&style=none&width=854)

### Q：支付宝预授权冻结接口无法调起支付，如何处理？

A：**可能原因**：

- 服务端回传的 tradeNO 出错，导致传入 my.tradePay 的 tradeNO 参数错误。
- 支付宝预授权无法在 IDE 模拟器中进行测试。

**解决方案**：

1. 可查看 [支付宝预授权](https://opendocs.alipay.com/mini/introduce/pre-authorization) 文档 **接入指引 > 第五步：调用接口 > 线上资金预授权冻结**，获取用于小程序支付的 orderStr 参数。
2. 将获得的 orderStr 参数传入  my.tradePay 中（设置为固定值），并在真机上进行测试。

### Q：支付宝预授权时，支付宝预授权报错”订单异常 ALIN42683”，如何处理？

A： **报错原因**：

OutOrderNo 和 OutRequestNo 重复请求。（OutOrderNo 和 OutRequestNo 参数详情可查看 [线上资金冻结场景](https://opendocs.alipay.com/mini/013ok0#%E7%BA%BF%E4%B8%8A%E8%B5%84%E9%87%91%E5%86%BB%E7%BB%93%E5%9C%BA%E6%99%AF)。）

**解决方案**：

1. 确保 OutOrderNo 和 OutRequestNo 入参在商家系统中唯一 （只传入 OutOrderNo 或只传入  OutRequestNo）。
2. 检查参数是否按照 [线上资金冻结场景](https://opendocs.alipay.com/mini/013ok0#%E7%BA%BF%E4%B8%8A%E8%B5%84%E9%87%91%E5%86%BB%E7%BB%93%E5%9C%BA%E6%99%AF) 要求设置，建议只传必传参数测试，避免其它参数干扰。

### Q：小程序支付无法调起支付，如何处理？

A：**可能原因**：

- 传入 my.tradePay 的   tradeNO  参数错误，导致服务端回传的 tradeNO 出错。
- 小程序支付无法在 IDE 模拟器中进行测试。

**解决方案**：

1. 在服务端调用 [alipay.trade.create](https://opendocs.alipay.com/mini/02j1c4)（统一收单交易创建接口），获得支付宝交易号 tradeNO。

> **注意**：在小程序场景内 alipay.trade.create 接口中的 buyer_id 为必填项，若未传入，则调试报错。推荐使用开放平台提供的 [服务端 SDK](https://opendocs.alipay.com/common/02n6z6) ，并参考以下示例代码（以 Java 代码为例）进行编写。

```java
// 实例化客户端
AlipayClient alipayClient = new     DefaultAlipayClient("https://openapi.alipay.com/gateway.do", APP_ID, APP_PRIVATE_KEY, "json", CHARSET, ALIPAY_PUBLIC_KEY, "RSA2");
// 实例化具体API对应的request类,类名称和接口名称对应,当前调用接口名称：alipay.trade.create.
AlipayTradeCreateRequest request = new AlipayTradeCreateRequest();
// SDK已经封装掉了公共参数，这里只需要传入业务参数。
request.setBizContent("{" +
        "\"out_trade_no\":\"20171115010101001\"," +
        "\"total_amount\":0.01," +
        "\"subject\":\"Iphone616G\"," +
        "\"buyer_id\":\"用户pid\"" +
        "}");
try {
    // 使用的是 execute
    AlipayTradeCreateResponse response = alipayClient.execute(request);
    String trade_no = response.getTradeNo();//获取返回的tradeNO。
} catch (AlipayApiException e) {
    e.printStackTrace();
}
```

2. 将获得的 tradeNO 参数传入  my.tradePay 中（设置为固定值），并在真机上进行测试。

### Q：小程序唤起支付可以支付其它 APPID 或者 PID 的订单吗？

A：小程序 my.tradePay 接口不会限制创建 tradeNO 交易号参数的应用 APPID，只要交易号合法即可。
