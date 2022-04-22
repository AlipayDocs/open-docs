
# 简介
**my.paySignCenter** 是用于在支付宝小程序内启动一个代扣 H5 服务的 API。

有关周期扣款更多信息，请参见 [周期扣款](https://opendocs.alipay.com/mini/006srl)。

## 使用限制

- 支付宝客户端 10.0.18 及以上版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 暂仅支持企业支付宝小程序使用。

# 接口调用

## 示例代码

### .axml 示例代码
```html
<!-- .axml -->
<view class="page">
  <view class="page-description">支付代扣签约</view>
  <view class="page-section">
    <view class="page-section-title">paySignCenter</view>
    <view class="page-section-demo">
      <button size="default" type="primary" onTap="paySignCenter">paySignCenter</button>
    </view>
  </view>
</view>
```

### .js 示例代码
```javascript
//.js
Page({
  data: {},
  onLoad() {},
  paySignCenter() {
    my.paySignCenter({
      signStr: 'alipay_sdk%3Dalipay-sdk-java-dynamicVersionNo%26app_id%3D2019072465924554%26biz_content%3D%257B%2522sign_validity_period%2522%253A%25222m%2522%252C%2522product_code%2522%253A%2522CYCLE_PAY_AUTH%2522%252C%2522external_logon_id%2522%253A%252213852852877%2522%252C%2522personal_product_code%2522%253A%2522CYCLE_PAY_AUTH_P%2522%252C%2522sign_scene%2522%253A%2522INDUSTRY%257CCARRENTAL%2522%252C%2522external_agreement_no%2522%253A%2522test%2522%252C%2522third_party_type%2522%253A%2522PARTNER%2522%252C%2522prod_params%2522%253A%257B%2522auth_biz_params%2522%253A%2522%257B%255C%2522platform%255C%2522%253A%255C%2522taobao%255C%2522%257D%2522%257D%252C%2522promo_params%2522%253A%2522%257B%255C%2522key%255C%2522%253A%255C%2522value%255C%2522%257D%2522%252C%2522access_params%2522%253A%257B%2522channel%2522%253A%2522ALIPAYAPP%2522%257D%252C%2522merchant_process_url%2522%253A%2522https%253A%252F%252Fwww.merchantpage.com%252Findex%253FprocessId%253D2345678%2522%252C%2522identity_params%2522%253A%257B%2522user_name%2522%253A%2522%25E5%25BC%25A0%25E4%25B8%2589%2522%252C%2522cert_no%2522%253A%252261102619921108888%2522%252C%2522identity_hash%2522%253A%25228D969EEF6ECAD3C29A3A629280E686CF0C3F5D5A86AFF3CA12020C923ADC6C92%2522%252C%2522sign_user_id%2522%253A%25222088202888530893%2522%257D%252C%2522agreement_effect_type%2522%253A%2522DIRECT%2522%252C%2522user_age_range%2522%253A%2522%257B%255C%2522min%255C%2522%253A%255C%252218%255C%2522%252C%255C%2522max%255C%2522%253A%255C%252230%255C%2522%257D%2522%252C%2522period_rule_params%2522%253A%257B%2522period_type%2522%253A%2522DAY%2522%252C%2522period%2522%253A9%252C%2522execute_time%2522%253A%25222022-05-23%2522%252C%2522single_amount%2522%253A10.99%252C%2522total_amount%2522%253A600%252C%2522total_payments%2522%253A12%257D%257D%26charset%3DUTF-8%26format%3Djson%26method%3Dalipay.user.agreement.page.sign%26sign%3Di8X5tQSVx%252Bj8UviKuGDz5Wc8lPf%252BBtOTzlEN2N60%252FFQp%252Fgk4pubIhMzq8duIyapCVJR74lE3GFIUHrTrvcMnaTFCyLp5gRWRQFWxxunAFEMvtSLA2HUbz7tnbg49o2aMHzpYLWgEtBDSR1yl8nLSNefm4iJ46evEFX4pNC%252FdXhW3PVWaOx6d8jIjEvTkaWBpYBG%252F%252BrFmS08xfMqR58hsWDAp7x7y7emgjEfVMmTQmKhLBY8BSfXrv%252BMX%252FwD5joOToloHpKVfhjeuHcpcmyPhLjX7SPpw9xaNnmEJa9ACrXhWk440Y9XT8XiB%252F68fRfPC%252FcU14kEiob5UK5AMwYnj3Q%253D%253D%26sign_type%3DRSA2%26timestamp%3D2022-04-22%2B11%253A04%253A20%26version%3D1.0',
      success: (res) => {
        my.alert({
          title: 'success', // alert框的标题
          content: JSON.stringify(res),
        })
      },
      fail: (res) => {
        my.alert({
          title: 'fail', // alert框的标题
          content: JSON.stringify(res),
        })
      },
    })
  },
})
```

## 入参
入参为 Object 类型，属性如下：

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| signStr | String | 是 | 签约字符串。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |


## 返回值
返回值为 JSON 格式，属性如下：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| result | JSON | 处理结果。 |
| resultStatus | String | 错误码，具体含义见下表。 |


### 返回值示例
```javascript
{
"result":"{
\"alipay_user_agreement_page_sign_response\":{
\"code\":\"10000\",
\"msg\":\"Success\",
\"app_id\":\"2017060101317939\",
\"auth_app_id\":\"2017060101317939\",
\"charset\":\"UTF-8\",
\"timestamp\":\"2017-06-27 11:40:15\",
\"sign_scene\":\"INDUSTRY|CARRENTAL\",
\"valid_time\":\"2017-06-27 11:40:13\",
\"status\":\"NORMAL\",
\"external_agreement_no\":\"test212\",
\"agreement_no\":\"20170627457298962889\",
\"external_logon_id\":\"13852852877\",
\"alipay_logon_id\":\"138****2877\",
\"invalid_time\":\"2017-08-27 11:40:13\",
\"personal_product_code\":\"GENERAL_WITHHOLDING_P\",
\"sign_time\":\"2017-06-27 11:40:14\",
},
\"sign":"KgeHoSYPuhpzhfrjeuwWbRmjJtlUp+5UGfq2OxYLraWEOqKsw9FokUnodMEgKgJK8=",
\"sign_type\":\"RSA\"
}",
"resultStatus":"7000"
}
```

## 错误码
| **错误码** | **描述** | **解决方案** |
| --- | --- | --- |
| 7000 | 协议签约成功。 | - |
| 7001 | 签约结果未知（有可能已经签约成功）。 | 请根据外部签约号查询签约状态。 |
| 7002 | 协议签约失败。 | 请稍后重试。 |
| 6001 | 用户中途取消。 | 请用户重新签约。 |
| 6002 | 网络连接错误。 | 请检查网络连接后重试。 |

