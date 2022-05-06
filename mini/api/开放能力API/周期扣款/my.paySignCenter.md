# 简介

**my.paySignCenter** 是用于在支付宝小程序内唤起周期扣款签约页面的 API。

![example.png](https://cdn.nlark.com/yuque/0/2022/png/179989/1649831018195-a839f066-fce5-4f8f-9a55-b00332c84a44.png)

有关周期扣款的签约流程、使用场景等更多信息，需要查看 [周期扣款](https://opendocs.alipay.com/mini/006srl)。

## 使用限制

- 支付宝客户端 10.0.18 及以上版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 暂不支持在 IDE 模拟器上调试，请以 [真机调试](https://opendocs.alipay.com/mini/ide/remote-debug) 结果为准。
- 此 API 暂仅支持企业支付宝小程序使用。
- 不支持在 IoT 小程序中使用。

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
// .js
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

入参为 Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| signStr | String | 是 | 签约字符串。请参考 [周期扣款 > 接入指南](https://opendocs.alipay.com/mini/012kfn#%E7%AC%AC%E4%BA%8C%E6%AD%A5%EF%BC%9AJSAPI%20%E5%94%A4%E8%B5%B7%E7%AD%BE%E7%BA%A6%E9%A1%B5%E9%9D%A2) 来获取该字符串。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

## 获取签约结果

返回值为 JSON 格式，属性如下：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| result | JSON | 处理结果。 |
| resultStatus | String | 错误码，具体含义见下表。 |

### success 回调结果示例

执行成功时，触发 success 回调，回调内容示例如下：

```javascript
{
    "result": "{\"alipay_user_agreement_page_sign_response\":{\"code\":\"10000\",\"msg\":\"Success\",\"app_id\":\"2017060101317939\",\"auth_app_id\":\"2017060101317939\",\"charset\":\"UTF-8\",\"timestamp\":\"2017-06-27 11:40:15\",\"sign_scene\":\"INDUSTRY|CARRENTAL\",\"valid_time\":\"2017-06-27 11:40:13\",\"status\":\"NORMAL\",\"external_agreement_no\":\"test212\",\"agreement_no\":\"20170627457298962889\",\"external_logon_id\":\"13852852877\",\"alipay_logon_id\":\"138****2877\",\"invalid_time\":\"2017-08-27 11:40:13\",\"personal_product_code\":\"GENERAL_WITHHOLDING_P\",\"sign_time\":\"2017-06-27 11:40:14\",},\"sign": "KgeHoSYPuhpzhfrjeuwWbRmjJtlUp+5UGfq2OxYLraWEOqKsw9FokUnodMEgKgJK8=\",\"sign_type\":\"RSA\"}",
    "resultStatus": "7000"
}
```

## 结果码

| **结果码** | **描述** | **解决方案** |
| --- | --- | --- |
| 7000 | 协议签约成功。 | - |
| 7001 | 签约结果未知（有可能已经签约成功）。 | 请根据外部签约号查询签约状态。 |
| 7002 | 协议签约失败。 | 请稍后重试。 |
| 6001 | 用户中途取消。 | 请用户重新签约。 |
| 6002 | 网络连接错误。 | 请检查网络连接后重试。 |

## 常见问题

### 1. 如何获取签约字符串？

调用 [alipay.user.agreement.page.sign](https://opendocs.alipay.com/mini/02fkb3?scene=35)（支付宝个人协议页面签约接口）传入周期扣款约定等相关信息创建签约协议内容。

将 SDK 的返回值中的 body 字段进行一次 urlencode 处理，将其结果做为 signStr 的值传入 my.paySignCenter。

示例以及详细信息请查看 [先签约，后代扣 > 创建签约协议内容](https://opendocs.alipay.com/mini/012kfn#%E7%AC%AC%E4%B8%80%E6%AD%A5%EF%BC%9A%E5%88%9B%E5%BB%BA%E7%AD%BE%E7%BA%A6%E5%8D%8F%E8%AE%AE%E5%86%85%E5%AE%B9) 。

请注意，示例代码中提到的 `alipayClient.pageExecute(request, 'get');` 这种方式会返回一个 URL 地址，您需要使用 `alipayClient.sdkExecute(request);` 的方式来获取正确的 signStr。

### 2. 唤起的签约界面显示 无效签名

请检查您传入的 signStr 是否正确。请对照以下内容进行自查：

传入的 signStr 需要形如：`alipay_sdk%3Dalipay-sdk-java-dynamicVersionNo%26app_id%3D2019072465924554%26biz_content%3D...`。

如果您是使用 SDK 获取的 signStr，您得到的是这样的字符串: `alipay_sdk=alipay-sdk-java-dynamicVersionNo&app_id=2019072465924554&biz_content=...`，需要先将这段字符串进行一次 urlencode。使用 Java SDK 示例代码如下：

```java
AlipayUserAgreementPageSignResponse response = alipayClient.sdkExecute(request);
String signStr = URLEncoder.encode(response.getBody(), "UTF-8");
```

### 3. 用户签约成功后回调显示报错 6001

如果要在小程序中使用，您发起的签约请求中不能带 return_url 字段。

因为您传了 return_url 导致签约完成后会跳到该 url，这样就跳出了小程序，您再回来小程序的时候，小程序的接口认为没有完成业务，所以就显示 6001 了。

小程序场景下 return_url 参数是不需要的，因为小程序接口本身有 success 回调方法，您直接在 success 回调方法中获取信息即可，不需要再指定 return_url。

### 4. 签约失败常见原因

1. 请检查您是否添加了对应的能力。
    请联系您的产品的支付宝业务经理BD为您添加对应的能力。
2. 请检查您调用 [alipay.user.agreement.page.sign](https://opendocs.alipay.com/mini/02fkb3?scene=35)（支付宝个人协议页面签约接口）时的参数是否正确，如 `product_code` 等。
