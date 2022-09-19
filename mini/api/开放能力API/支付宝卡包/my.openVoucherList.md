# 简介

**my.openVoucherList** 打开支付宝卡包并显示优惠券列表。

有关支付宝卡包详细功能，可查看 [支付宝卡包产品介绍](https://opendocs.alipay.com/open/199/105225)。

## 使用限制

此 API 暂仅支持企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码

```javascript
my.openVoucherList({
  complete: () => {
    console.log('openVoucherList complete')
  }
});
```
