# 简介

**my.openCardDetail** 是打开当前用户的某张卡的详情页的 API。

有关支付宝卡包详细功能，可查看 [支付宝卡包产品介绍](https://opendocs.alipay.com/open/199/105225)。

支付宝特色   API，支持 my.ap.openCardDetail 调用。

## 使用限制

此 API 暂仅支持企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码

```javascript
// .js
//传入passId来打开
my.openCardDetail({ passId: '11xxxxx' });
```

## 入参

Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| passId | String | 是 | 卡实例 ID。<br />**passId 获取方式**： <ol><li>通过 alipass 创建的卡：<br />调用 [alipay.pass.instance.add](https://opendocs.alipay.com/open/02ailb)（卡券实例发放接口），在出参“result”中可获取。</li><li>通过会员卡创建的卡：<br />调用 [alipay.marketing.card.query](https://opendocs.alipay.com/open/02dvep)（会员卡查询接口），在 scheme_url 中可获取，具体参数为“p=xxx”，xxx 即为 passId。</li></ol> |
