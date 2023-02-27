## 错误码
ITEM_HAS_EXIST（商品已经存在）。 

## 错误描述
调用 alipay.merchant.order.sync（订单数据同步接口）来同步更新订单状态时报错："sub_code": "ITEM_HAS_EXIST","sub_msg": "商品已经存在"。 

## 涉及接口

- [alipay.merchant.order.sync](https://opendocs.alipay.com/mini/043zb5)（订单数据同步接口）
- ant.merchant.expand.item.create（商品创建接口）
- ant.merchant.expand.item.modify（商品修改接口）

## 报错原因
该同步的订单已经同步至订单中心，item_order_list 不可传。 

## 解决方案
订单商品信息已经通过支付链路同步，无法修改。若要同步其它信息请确保商品信息 item_order_list 为空不可传。
