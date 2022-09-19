# 简介

**my.openVoucherList** 是查看支付宝卡包中优惠券的 API。

有关支付宝卡包详细功能，可查看 [支付宝卡包产品介绍](https://opendocs.alipay.com/open/199/105225)。

## 使用限制

此 API 暂仅支持企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码

```javascript
// .js
my.openVoucherList({
  success: (res) => {
    console.log('调用成功', res)
  },
  fail: (error) => {
    console.log('调用失败', error)
  },
  complete: () => {
   console.log('调用完成，无论是否成功都会执行')
  }
});
```
