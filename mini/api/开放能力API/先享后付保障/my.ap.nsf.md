# 简介
**my.ap.nsf** 是根据用户身份特征以及行为信息，判断用户在先享后付场景下是否有风险的 API。

有关先享后付保障更多信息，可查看 [先享后付保障](https://opendocs.alipay.com/mini/introduce/non-sufficient-funds)。

## 使用限制

- 基础库 [1.14.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.52 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 暂仅支持企业支付宝小程序使用。

## 评级说明
| **评级** | **描述** | **处理建议** |
| --- | --- | --- |
| rank0 | 提供信息不足，提供参数信息有误，或提供的支付宝账号不存在。 | 请检查入参信息。 |
| rank1 | 用户拒付风险为低。 | 用户可以先享受服务，再进行支付。 |
| rank2 | 用户拒付风险为中。 | 根据业务场景客户自行判断提供或者不提供。 |
| rank3 | 用户拒付风险为高。 | 不建议先提供给用户服务。 |

# 接口调用

## 示例代码

### .js 示例代码
```javascript
// .js
my.ap.nsf({
  // 请自行替换 xxxxx 各个参数
  pid:'xxxxxxxxxxxxxxxx',
  appId:'xxxxxxxxxxxxxxxx',
  bizContext: {
        "risk_type": "riskinfo_nsf_common", 
        "user_id": "xxxxxxxxxxxxxxxx", 
        "lbs": "xx.xxxxxxxxxxxxx", 
        "sales_amount": "xx", 
        "mobile_no": "null", 
        "pid": "xxxxxxxxxxxxxxx",
        "cert_no": "xxxxxxxxxxxxxxxxxxx"
  },
  success(e) {
  },
})
```

## 入参
Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| pid | String | 是 | 小程序的开放平台账号。 |
| appId | StringArray | 是 | 小程序对应的 appId。 |
| bizContext | Map | 是 | 需要识别的业务参数。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

### Map bizContext
| **属性** | **类型** | **必填** | **最大长度** | **描述** | **示例值** |
| --- | --- | --- | --- | --- | --- |
| risk_type | String | 是 | 1024 | 用于代表商家风险类型，固定传入 riskinfo_nsf_common，请按示例值填写。 | 固定传入riskinfo_nsf_common |
| pid | String | 是 | 128 | 商家的小程序开放平台账号。 | 2088345256451234 |
| user_id | String | 是 | 128 | 用于输入用户支付宝的 2088 账号，如不了解此字段如何获取，可了解下静默授权。如参数无法提供，请填写“null”。 | 2088501624560335 |
| mobile_no | String | 是 | 128 | 用于输入用户注册支付宝的手机号码。如参数无法提供，请填写“null”。 | 13810935692 |
| cert_no | String | 否 | 128 | 用于输入用户身份证号。如参数无法提供，请填写“null”。 | 13810935692 |
| lbs | String | 否 | 128 | 用于输入用户产生交易时的地理位置信息。如参数无法提供，请填写“null”。 | 30.2727707248263 |
| sales_amount | String | 否 | 128 | 用户购买或使用服务时产生的具体金额。如参数无法提供，请填写“null”。 | 97.23 |

### Function success
success 回调函数会携带一个 Object 类型的对象，其属性如下：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| result | Object | 风险识别的返回结果。 |

#### Object result
| **属性** | **类型** | **描述** | **示例值** |
| --- | --- | --- | --- |
| riskResult | String | 风险识别结果。<br />riskinfo_nsf_common 风险评级结果：<ul><li>rank0 提供信息不足，提供参数信息有误，或提供的支付宝账号不存在。</li><li>rank1 表示用户拒付风险为低。</li><li>rank2 表示用户拒付风险为中。</li><li>rank3 表示用户拒付风险为高。</li></ul> | {\"riskinfo_nsf_common\":\"rank1\"} |
| riskResultDesc | String | 风险信息描述。 | {\"rank0\":\"等级0\"} |
| uniqueId | String | 业务唯一识别码。<br />用户标识请求信息。 | 0b92uueie87636222 |


### Function fail
fail 回调函数会携带一个 Object 类型的对象，其属性如下：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| error | String | 错误码。 |
| errorMessage | String | 错误信息。 |

## 错误码
| **错误码** | **描述** | **解决方案** |
| --- | --- | --- |
| serviceNoAuth | 服务未授权。 | 请检查配置的账户是否有当前接口权限； service 参数是否正确。 |
| riskTypeNoAuth | 场景（risktype）未授权。 | 请检查 risktype 参数是否正确。 |
| bizContentEmpty | 风险数据内容为空。 | 检查入参数据格式。 |
| paramMissingError | 参数缺失。 | 检查必传参数是否传入。 |
| param error | 参数错误。 | 检查入参格式是否符合文档要求。 |
| SYSTEM_OUT_ERROR | 系统繁忙。 | 请稍后再试。 |
| INVALID_PARAMETER | 缺少必选参数或参数有误。 | 检查参数是否正确或者缺失。 |
| OVER_LIMIT | 超过调用量限制。 | 如需增加额度，请发邮件至 `RiskGoCSC@service.alipay.com` 进行申请。 |

# 常见问题 FAQ

## Q：my.ap.nsf 中的两个 pid 是否传一致的参数？ 
A：两者 pid 相同。
