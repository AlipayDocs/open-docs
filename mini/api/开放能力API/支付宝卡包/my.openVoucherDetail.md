# 简介

**my.openVoucherDetail** 是打开当前用户的某张券的（非口碑）详情页的 API，打开支付宝券详情页。

有关支付宝卡包详细功能，可查看 [支付宝卡包产品介绍](https://opendocs.alipay.com/open/199/105225)。

## 使用限制

- 此 API 暂仅支持企业支付宝小程序使用。
- 此 API 暂不支持打开口碑券的详情页，若想打开口碑券的详情页，请使用 [my.openKBVoucherDetail](https://opendocs.alipay.com/mini/api/tfa5s0) 接口。

# 接口调用

## 示例代码

### .js 示例代码

```javascript
// 传入passId来打开
my.openVoucherDetail({ 
  passId: '20170921',
  success: (res) => {
    console.log('调用成功', res)
  },
  fail: (error) => {
    console.log('调用失败', error)
  },
  complete: () => {
    console.log('调用完成，无论成功或者失败都会调用')
  }
});
// 传入partnerId 和 serialNumber来打开
my.openVoucherDetail({
  partnerId: '2018xxxx',
  serialNumber: '20170921',
  success: (res) => {
    console.log('调用成功', res)
  },
  fail: (error) => {
    console.log('调用失败', error)
  },
  complete: () => {
    console.log('调用完成，无论成功或者失败都会调用')
  }
});
```
## 示例效果图
![avatar](https://img.alicdn.com/imgextra/i2/O1CN014SXvf226BqOVOigEg_!!6000000007624-0-tps-592-1280.jpg)

## 入参

Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| passId | String | 是 | 券实例 ID，调用 [alipay.pass.instance.add](https://opendocs.alipay.com/open/02ailb)（卡券实例发放接口）可以获取该参数（如果传入了 partnerId 和 serialNumber 则不需传入）。 |
| partnerId | String | 是 | 商户编号，即商户 PID。<br> PID 即 Partner ID，是商家与支付宝签约后所获得的唯一识别码，由 16 位数字组成，以 2088 开头。<br>PID 的获取可查看文档：[获取PID](https://opendocs.alipay.com/common/02ncut)（如果传入了 passId 则不需传入）。 |
| serialNumber | String | 是 | 序列号，调用 [alipay.pass.template.add](https://opendocs.alipay.com/open/02aila)（卡券模板创建接口）可以获取该参数（如果传入了 passId 则不需传入）。 |
