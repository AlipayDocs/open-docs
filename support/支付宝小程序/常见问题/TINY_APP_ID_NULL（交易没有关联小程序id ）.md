## 错误码
TINY_APP_ID_NULL（交易没有关联小程序id ）。 

## 错误描述
调用alipay.merchant.order.sync（订单数据同步接口）接口来同步更新订单状态时出现：“"sub_code": "TINY_APP_ID_NULL","sub_msg": "交易没有关联小程序id"”报错。 

## 涉及接口
[alipay.merchant.order.sync](https://opendocs.alipay.com/mini/84f9ee3c_alipay.merchant.order.sync?scene=common&pathHash=103117c9)（订单数据同步接口）。 

## 报错原因
同步的订单交易没有在小程序中唤起收银台完成支付，是小程序外的渠道唤起的支付。例如：小程序创建交易后在个人账单中会有一笔待支付的记录，用户可能在账单中支付的这笔订单。 

## 解决方案

- 导入订单必须为用户在小程序内下单支付的订单且回传订单信息包含商品图片、商品名称、订单详情url，否则在订单中心列表页不会展示（系统会自动识别交易来源是否为小程序）。
- 请使用关联了小程序的交易同步订单信息，可在订单同步接口参数 ext_info 中入参订单归属的小程序 appid。
