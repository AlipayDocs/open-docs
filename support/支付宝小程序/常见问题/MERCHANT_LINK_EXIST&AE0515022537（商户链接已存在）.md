## 错误码
MERCHANT_LINK_EXIST（商户链接已存在）。 

## 错误描述
调用 alipay.merchant.order.sync（订单数据同步接口）来同步更新订单状态时报错："sub_code": "MERCHANT_LINK_EXIST","sub_msg": "商户链接已存在"或"sub_code":"AE0515022537","sub_msg":"商户链接已存在"。 

## 涉及接口
[alipay.merchant.order.sync](https://opendocs.alipay.com/mini/043zb5)（订单数据同步接口）

## 报错原因
接口中请求 merchant_order_link_page 与已存不一致。 

## 解决方案
[alipay.merchant.order.sync](https://opendocs.alipay.com/mini/043zb5)（订单数据同步接口）的 ext_info 参数设置 merchant_order_link_page 参数导致，merchant_order_link_page 参数整个流程中只能传一次，不允许修改更新，去掉 merchant_order_link_pag e参数即可。<br /> <br /> 
