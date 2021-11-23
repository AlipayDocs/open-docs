
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
      signStr: 'biz_content%3D%257B%2522access_params%2522%253A%257B%2522channel%2522%253A%2522ALIPAYAPP%2522%257D%252C%2522external_agreement_no%2522%253A%2522xidong___2317%2522%252C%2522external_logon_id%2522%253A%252213852852877%2522%252C%2522personal_product_code%2522%253A%2522GENERAL_WITHHOLDING_P%2522%252C%2522product_code%2522%253A%2522GENERAL_WITHHOLDING%2522%252C%2522sign_scene%2522%253A%2522INDUSTRY%257CCARRENTAL%2522%252C%2522third_party_type%2522%253A%2522PARTNER%2522%257D%26sign%3Df3pjBDTRftOwXWnCqAMAnkBfGTFlcMmZI8hEgmV6uREZRXVDuLsSjD8WO%252FeZ1fjDG8GqVO9t1AN7q6yCUHKX%252Bw%252FE7efXwpVDWldr4iVuXDtNd3UJDJUiRJhIm6b73czWacVzm1XIery%252F2DyKI2y08tBf5NNWuQCC3d%252FITxziTl8%253D%26timestamp%3D2017-06-27%2B14%253A44%253A00%26sign_type%3DRSA%26notify_url%3Dhttp%253A%252F%252Fapi.test.alipay.net%252Fatinterface%252Freceive_notify.htm%26charset%3DUTF-8%26app_id%3D2017060101317939%26method%3Dalipay.user.agreement.page.sign%26return_url%3Dhttp%253A%252F%252Fapi.test.alipay.net%252Fatinterface%252Freceive_notify.htm%26version%3D1.0',
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

