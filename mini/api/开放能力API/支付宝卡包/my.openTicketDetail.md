# 简介
**my.openTicketDetail** 是打开当前用户的某张票的详情页的 API。

有关支付宝卡包详细功能，可查看 [支付宝卡包产品介绍](https://opendocs.alipay.com/mini/introduce/voucher)。

支付宝特色 API，支持 my.ap.openTicketDetail 调用。

## 使用限制
此 API 暂仅支持企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码
```javascript
// .js
//传入passId来打开
my.openTicketDetail({passId:"20170921"}); 
// 传入partnerId 和 serialNumber来打开
my.openTicketDetail({
  partnerId:"2088xxxx",
  serialNumber:"20170921"
});
```

## 入参
Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| passId | String | 是 | 卡实例 ID（如果传入了 partnerId 和 serialNumber 则不需要传入 passId ）。 |
| partnerId | String | 是 | 商户编号（即商户 PID，如果传入了 passId 则不需要传入 partnerId）。 |
| serialNumber | String | 是 | 序列号（如果传入了 passId 则不需要传入 serialNumber）。 |
