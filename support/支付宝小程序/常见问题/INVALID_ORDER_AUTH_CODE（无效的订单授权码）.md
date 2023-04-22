## 错误码
INVALID_ORDER_AUTH_CODE（无效的订单授权码）。 

## 错误描述
调用 alipay.merchant.order.sync（订单数据同步接口）来同步更新订单状态时报错："sub_code": "INVALID_ORDER_AUTH_CODE","sub_msg": "无效的订单授权码"。 

## 涉及接口
[alipay.merchant.order.sync](https://opendocs.alipay.com/mini/043zb5)（订单数据同步接口）

## 报错原因
order_auth_code 中的信息与传入的 tiny_app_id 与 buyer_id 不一致导致。 

## 解决方案

- 请确保 order_auth_code 中的信息与传入的 tiny_app_id 与 buyer_id 一致。订单同步前获取的 formId 作为订单授权码。订单授权码对应的小程序 id 与买家 uid 与同步订单的小程序 id 和买家 uid 一致。<br />订单授权码(与订单一一对应，不是请求维度的，服务订单首次同步必传。
- 同步非交易新订单需传入小程序 appid、用户 UID 及 formid，请确保该 formid 正确且是当前用户所产生，以及未使用该 ID 同步订单，系统会校验 ID 的合法性及可用性；若该 ID 和用户 UID 不符、ID 已同步订单，则无法同步订单。<br />**注意：**当 order_type 为 SERVICE_ORDER 时，该参数必填；商家可传入 formId，formId 通过 form 表单组件来获取，详情可查看[ ](https://opendocs.alipay.com/mini/component/form#%E5%B1%9E%E6%80%A7)[小程序前端如何通过form表单获取formId](https://opendocs.alipay.com/support/01rb7y#)。

