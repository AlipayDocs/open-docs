## 错误码
NO_PERMISSOON（没有权限）。 

## 错误描述
调用接口报错："sub_code": "NO_PERMISSOON","sub_msg": "没有权限"。 

## 涉及接口
[alipay.merchant.order.sync](https://opendocs.alipay.com/mini/043zb5)（订单数据同步接口）

## 报错原因
订单 PID 与交易 PID 不一致导致。 

## 解决方案

- seller_id 和 partner_id 入参相同时：
   - 确认该账号是否已经来通了小程序订单中心产品。
   - 确认同步的支付宝交易 trade_no 是否是属于该 PID 账号下的交易。 
- seller_id 和 partner_id 入参不相同时：
   - 确认 partner_id 入参的账户 PID 是否已经开通了小程序订单中心产品。
   - 确认同步的支付宝交易 trade_no 是否是属于 seller_id 入参的账户 PID 下的交易。

**注意：**

- 小程序订单中心开通确认可使用对应账号登录开放平台确认。
- 可通过 [alipay.trade.query](https://opendocs.alipay.com/open/02ekfh)（统一收单线下交易查询接口）查询该支付宝交易信息。
