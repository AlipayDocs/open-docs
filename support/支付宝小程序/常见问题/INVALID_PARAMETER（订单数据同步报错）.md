
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

## 1. 订单状态错误

### 1.1 服务订单订单状态不可空
字段 merchant_order_status（订单状态）没有传入。

### 1.2 订单状态不合法
回流的订单状态不在订单模板支持的状态集内。请根据 [业务场景对接开发文档](https://opendocs.alipay.com/mini/04zsxt) 同步正确的状态。

### 1.3 订单状态乱序
订单回流时，出现逆向的状态流转，例如状态从 FINISHED -> CREATE，建议查看 [业务场景对接开发文档](https://opendocs.alipay.com/mini/04zsxt) 的订单状态流转图，检查订单同步时的状态顺序是否正确。

## 2. 订单金额错误

### 2.1 订单金额不等于支付金额加优惠金额
订单金额需等于支付金额加优惠金额（即：amount = pay_amount + discount_amount ）
- amount：订单金额。
- pay_amount：支付金额。
- discount_amount：优惠金额。

**说明：**

- 支付金额为优惠前的金额。若使用了支付宝交易，该字段使用支付宝交易信息中的 total_amount 的金额（发起支付时的金额）。
- 当不涉及金额，可不传入 amount 、 pay_amount 、discount_amount ；如果有涉及金额，amount = pay_amount + discount_amount 。
- 当传入了 trade_no 时，pay_amount 的值要求与支付宝交易信息中的 total_amount 的金额相等。

### 2.2 支付金额与实际交易金额不一致
支付金额为 pay_amount ，指优惠前的金额。若使用了支付宝交易，该字段使用支付宝交易信息中的 total_amount 的金额。<br />**说明：**
当传入了 trade_no 时，pay_amount 的值要求与支付宝交易信息中的 total_amount 的金额相等。

## 3. 订单时间错误

### 3.1 业务修改时间不能早于业务创建时间
order_modified_time 必须晚于 order_create_time。

**说明：**

- order_modified_time：订单修改时间。
- order_create_time：订单创建时间。

### 3.2 短时间内重复请求，幂等拦截
当订单有变更时候再同步数据，注意订单变更后修改 order_modified_time（订单修改时间）字段值。

### 3.3 business_info 中的 charging_start_time 已设置不可更改
此订单已存在，business_info 中的 charging_start_time 须保持一致，不允许更改。

**说明：**

- business_info：业务信息参数。
- charging_start_time：充电开始时间。

## 4. 商品信息错误

### 4.1 商品名称不能为空
字段 item_name（商品名称）不能为空。

### 4.2 缺少必填属性：item_order_list.item_name
item_order_list 中的 item_name 不能为空。

**说明：**

- item_order_list：商品信息列表。
- item_name：商品名称。

## 5. 买家信息错误

### 5.1 买家信息不能为空
字段 buyer_id 没有传入。

**说明：**

- buyer_id 为支付宝用户 UID 。
- 由于历史原因，buyer_id 与 buyer_info 必选其一。现在新接入的商家，要求 buyer_id 必传，buyer_info 不传。

### 5.2 订单买家与交易买家不一致
订单同步时，回流了 trade_no 后，buyer_id 需要和 trade_no 中对应交易的买家信息保持一致。

**说明：**

- trade_no：订单对应的支付宝交易号。
- buyer_id：支付宝用户买家 UID。

## 6. 交易号错误

### 6.1 交易号已存在于另外一笔订单中
同步订单时，每个订单使用的 trade_no（支付宝交易号）不能重复。

### 6.2 交易不存在
没有查到回传的 trade_no（支付宝交易号），请确认 trade_no（支付宝交易号）是否正确。

## 7. 外部订单号错误

### 7.1 外部订单号与订单记录 id 不能同时为空
record_id 或 out_biz_no 不能同时为空。

**说明：**

- out_biz_no：外部订单号。
- record_id：订单记录 id。

### 7.2 幂等失败（存在不同 subBizType）
订单模板不能修改。请检查该笔 out_biz_no 是否已在其他 merchant_biz_type 下进行了回流。

**说明：**

- out_biz_no：外部商家订单号。
- merchant_biz_type：订单模板类型。

### 7.3 业务订单号不能为空
out_biz_no（外部商家订单号）不能为空。

**如果以上内容依然不能帮助您解决问题，请加入支付宝订单中心对接群，打开钉钉搜索群号 31604424，尝试联系 支付宝技术支持 获得帮助。**
