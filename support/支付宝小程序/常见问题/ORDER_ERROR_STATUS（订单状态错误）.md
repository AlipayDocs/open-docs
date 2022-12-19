## 错误码
ORDER_ERROR_STATUS（订单状态错误）。 

## 错误描述
调用alipay.merchant.order.sync（订单数据同步接口）接口来同步更新订单状态时出现：“"sub_code": "ORDER_ERROR_STATUS","sub_msg": "订单状态错误"”报错。 

## 涉及接口
[alipay.merchant.order.sync](https://opendocs.alipay.com/mini/043zb5)（订单数据同步接口）。 

## 报错原因
merchant_order_status 同步的状态不按顺序同步或跨状态调用。 

## 解决方案

- 在使用该接口时，同一笔订单在同一个 merchant_order_status 状态下只能调用一次接口，第二次调用会报错 **订单状态错误**；订单状态必须按照 **已付款** > **已确认** > **服务中**/**发货中** > **已完成** 的顺序同步，跨状态调用也会出现 **订单状态错误** 的报错。<br />**说明：**交易订单异步同步时若无需中间状态，如 **已确认**、**服务中**、**发货中** ，可直接跳过中间态直接同步已完成状态。
- 非交易订单同步时，请勿使用和支付相关的状态。

 
