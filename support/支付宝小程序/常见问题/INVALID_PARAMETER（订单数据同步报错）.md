
# 错误描述
小程序 [订单中心](https://opendocs.alipay.com/mini/introduce/ordercenter?ref=api) 提示 INVALID_PARAMETER（参数有误，不同情况下的 sub_msg 可能不同）。
```json
{"xxx_response":{"code":"40004","msg":"Business Failed","sub_code":"INVALID_PARAMETER","sub_msg":"xxx"},"sign":"***"}
```

# 涉及接口
[alipay.merchant.order.sync](https://opendocs.alipay.com/mini/043zb5?ref=api)（订单数据同步接口）

# 错误原因
参数填写有误，不符合当前场景下对入参的约束。<br />具体不同场景下有不同的原因，请查看以下解决方案。

# 解决方案
支付宝订单中心回传订单使用统一接口：alipay.merchant.order.sync ，因为各行业差异较大，在回传订单时，回参请参照具体业务场景的开发文档进行开发。详情可查看 [行业订单模板列表](https://opendocs.alipay.com/mini/04zsxt)。<br />不同情况下的解决方案不同，常见的 sub_msg 对应的解决方案见下。

## 参数有误

### 服务订单订单状态不可空
字段 merchant_order_status（订单状态）没有传入。

### 买家信息不能为空
字段 buyer_id 没有传入。<br />**说明：**

- buyer_id 为支付宝用户 UID 。
- 由于历史原因，buyer_id 与 buyer_info 必选其一。现在新接入的商家，要求 buyer_id 必传，buyer_info 不传。

### 订单金额不等于支付金额加优惠金额
订单金额需等于支付金额加优惠金额（即：amount = pay_amount + discount_amount ）

- amount：订单金额。
- pay_amount：支付金额。
- discount_amount：优惠金额。

**说明：**

- 支付金额为“支付相关优惠”前的金额。若使用了支付宝交易，该字段使用支付宝交易信息中的 total_amount 的金额（发起支付时的金额）。
- 当不涉及金额，可不传入 amount 、 pay_amount 、discount_amount ；如果有涉及金额，amount = pay_amount + discount_amount 。
- 当传入了 trade_no 时，pay_amount 的值要求与支付宝交易信息中的 total_amount 的金额相等。

### 支付金额与实际交易金额不一致
支付金额为 pay_amount ，指“支付相关优惠”前的金额。若使用了支付宝交易，该字段使用支付宝交易信息中的 total_amount 的金额。<br />**说明：**当传入了 trade_no 时，pay_amount 的值要求与支付宝交易信息中的 total_amount 的金额相等。

### 外部订单号与订单记录 id 不能同时为空
record_id 或 out_biz_no 不能同时为空。<br />**说明：**

- out_biz_no：外部订单号。
- record_id：订单记录 id 。

### 商品名称不能为空
字段 item_name（商品名称）不能为空。

### 缺少必填属性：item_order_list.item_name
item_order_list 中的 item_name 不能为空。<br />**说明：**

- item_order_list：商品信息列表。
- item_name：商品名称。

### <br />
