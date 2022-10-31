# 简介

**my.openKBVoucherDetail** 是用于打开当前用户的某张口碑券详情页的 API。

有关支付宝卡包详细功能，参见 [支付宝卡包产品介绍](https://opendocs.alipay.com/open/199/105225)。



## 使用限制

- 此 API 暂仅支持企业支付宝小程序使用。
- 此 API 只能打开口碑发放的券的详情页面。

# 接口调用

## 示例代码

### .js 示例代码

```javascript
// 使用 passId 打开
my.openKBVoucherDetail({ 
  passId: 'xxxxxxxx',
  success: (res) => {
    console.log('调用成功', res);
  },
  fail: (error) => {
    console.log('调用失败', error);
  }
});

// 使用 partnerId 和 serialNumber
my.openKBVoucherDetail({
  partnerId: '2088xxxx',
  serialNumber: '20170921',
  success: (res) => {
    console.log('调用成功', res);
  },
  fail: (error) => {
    console.log('调用失败', error);
  }
});
```
## 示例效果图
![avatar](https://img.alicdn.com/imgextra/i4/O1CN01B0ccFW23CoNiRSxhQ_!!6000000007220-0-tps-592-1280.jpg)

## 入参

Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| passId | String | 是 | 卡实例 ID（如果传入了 partnerId 和 serialNumber 则不需传入）。 |
| partnerId | String | 是 | 商户编号，即商户 PID。<br> PID 即 Partner ID，是商家与支付宝签约后所获得的唯一识别码，由 16 位数字组成，以 2088 开头。<br>PID 的获取可查看文档：[获取PID](https://opendocs.alipay.com/common/02ncut)（如果传入了 passId 则不需传入）。 |
| serialNumber | String | 是 | 序列号（如果传入了 passId 则不需传入）。 |
