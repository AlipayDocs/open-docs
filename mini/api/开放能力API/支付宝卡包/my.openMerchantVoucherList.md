# 简介
**my.openMerchantVoucherList** 是打开当前用户的某个商户的券列表的 API。

打开支付宝卡列表。有关支付宝卡包详细功能，可查看 [支付宝卡包产品介绍](https://opendocs.alipay.com/mini/introduce/voucher)。

## 使用限制
此 API 暂仅支持企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码
```javascript
// .js
my.openMerchantVoucherList({partnerId:'2088xxxx'});
```

## 入参
Object 类型，参数如下：

| **参数**  | **类型** | **必填** | **描述**               |
| --------- | -------- | -------- | ---------------------- |
| partnerId | String   | 是       | 商户编号，即商户 PID。 |
