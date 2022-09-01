# 简介

**my.openMerchantTicketList** 是打开某个商户的票列表的 API。

有关支付宝卡包详细功能，可查看 [支付宝卡包产品介绍](https://opendocs.alipay.com/open/199/105225)。

支付宝特色 API，支持 my.ap.openMerchantTicketList 调用。

## 使用限制

此 API 暂仅支持企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码

```javascript
// .js
my.openMerchantTicketList({ partnerId: '2088xxxx' });
```

## 入参

Object 类型，参数如下：

| **参数**  | **类型** | **必填** | **描述**               |
| --------- | -------- | -------- | ---------------------- |
| partnerId | String   | 是       | 商户编号，即商户 PID。 |
