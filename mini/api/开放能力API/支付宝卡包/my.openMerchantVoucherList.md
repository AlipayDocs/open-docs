# 简介

**my.openMerchantVoucherList** 是打开当前用户的某个商户的券列表的 API。

打开支付宝卡列表。有关支付宝卡包详细功能，可查看 [支付宝卡包产品介绍](https://opendocs.alipay.com/open/199/105225)。

## 使用限制

此 API 暂仅支持企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码

```javascript
// .js
my.openMerchantVoucherList({ 
  partnerId: '2088xxxx',
  success: (res) => {
    console.log('调用成功后的回调', res)
  },
  fail: (error) => {
    console.log('调用失败后的回调', error)
  },
  complete: ()=>{
    console.log('调用完成')
  }
});
```

## 入参

Object 类型，参数如下：

| **参数**  | **类型** | **必填** | **描述**               |
| --------- | -------- | -------- | ---------------------- |
| partnerId | String   | 是       | 商户编号，即商户 PID。 PID：全称：Partner ID，是合作者身份 ID，是商家与支付宝签约后，商家获得的支付宝商家唯一识别码，以 2088 开头的 16 位数字组成。PID 的获取可查看文档：[获取PID](https://opendocs.alipay.com/common/02ncut)|
