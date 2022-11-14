# 简介

**my.openMerchantCardList** 是打开当前用户的某个商户的卡列表的 API。

有关支付宝卡包详细功能，可查看 [商家会员卡产品介绍](https://opendocs.alipay.com/open/03sx7r?ref=api)。


## 使用限制

此 API 暂仅支持企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码

```javascript
// .js
my.openMerchantCardList({
  partnerId: '2088xxxxxxxxx',
  success: (res) => {
    console.log('调用成功', res)
  },
  fail: (error) => {
    console.log('调用失败', error)
  },
  complete: () => {
    console.log('调用完成，无论成功失败都会执行')
  }
});
```
### 示例效果图
![avatar](https://img.alicdn.com/imgextra/i4/O1CN01x7oo0P1G3jM4t5pNE_!!6000000000567-2-tps-634-652.png)

## 入参

Object 类型，参数如下：

| **参数**  | **类型** | **必填** | **描述**   |
| --------- | -------- | -------- | ---------- |
| partnerId | String   | 是       | 商户编号，即商户 PID。<br> PID 即 Partner ID，是商家与支付宝签约后所获得的唯一识别码，由 16 位数字组成，以 2088 开头。<br>PID 的获取可查看文档：[获取PID](https://opendocs.alipay.com/common/02ncut)。 |
