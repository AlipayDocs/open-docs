## 错误码
DATA_ACCESS_EXCEPTION（数据库访问异常）。 

## 错误描述
调用 alipay.merchant.order.sync（订单数据同步接口）来同步更新订单状态时报错："sub_code": "DATA_ACCESS_EXCEPTION","sub_msg": "数据库访问异常"。 

## 涉及接口
[alipay.merchant.order.sync](https://opendocs.alipay.com/mini/043zb5)（订单数据同步接口）

## 报错原因
很有可能为数据库唯一性破坏异常。 

## 解决方案
请确保 order_auth_code 唯一，或者 pay_biz_no + buyer_id 唯一。

- order_auth_code 所传入 formId，每个 formId 只能同步一个订单，同一用户有多个订单时请重新生成新的 formId 入参 order_auth_code，确保 order_auth_code 唯一。<br />**说明：**确保 order_auth_code 中的信息与传入的 tiny_app_id 与 buyer_id 一致，formId获取，详情可查看[ ](https://opendocs.alipay.com/mini/component/form#%E5%B1%9E%E6%80%A7)[小程序前端如何通过form表单获取formId](https://opendocs.alipay.com/support/01rb7y#)。
-  每个 trade_no 一个支付宝交易号只能同步一个订单，注意不要重复连续同步同一个交易号，确保 pay_biz_no + buyer_id 唯一。

