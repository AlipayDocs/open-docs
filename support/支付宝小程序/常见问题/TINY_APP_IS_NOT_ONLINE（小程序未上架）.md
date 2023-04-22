## 错误码
TINY_APP_IS_NOT_ONLINE（小程序未上架）。 

## 错误描述
调用alipay.merchant.order.sync（订单数据同步接口）来同步更新订单状态时报错："sub_code": "TINY_APP_IS_NOT_ONLINE","sub_msg": "小程序未上架"。 

## 涉及接口
[alipay.merchant.order.sync](https://opendocs.alipay.com/mini/043zb5)（订单数据同步接口）。 

## 报错原因
小程序未上架过。 

## 解决方案
同步非交易订单时需要小程序为已上架的小程序，请上架小程序后再调用。<br /> <br /> 
