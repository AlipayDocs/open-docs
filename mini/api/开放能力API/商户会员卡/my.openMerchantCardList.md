# 简介
**my.openMerchantCardList** 是打开当前用户的某个商户的卡列表的 API。

有关支付宝卡包详细功能，可查看 [支付宝卡包产品介绍](https://opendocs.alipay.com/open/199/105225)。

支付宝特色 API ，支持 my.ap.openMerchantCardList 调用。

## 使用限制
此 API 暂仅支持企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码
```javascript
// .js
my.openMerchantCardList({partnerId:'2088xxxxx'});
```

## 入参
Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| partnerId | String | 是 | 商户编号。 |
