# 简介
**my.ap.preventCheat** 是用于调用反作弊接口，根据入参说明来传参，接口会返回当前用户的风险识别结果，开发者可根据结果来做相应业务处理。

有关营销反作弊的产品和接入介绍，可查看 [营销反作弊](https://opendocs.alipay.com/mini/introduce/antimarketcheat)。

## 使用限制

- 基础库 [1.12.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.38 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 暂仅支持企业支付宝小程序使用。

## 风险识别结果
| **风险评级结果** | **描述** | **处理方案** |
| --- | --- | --- |
| rank0 | 表示信息不足或提供的参数有误。 | 请检查入参信息。 |
| rank1 | 表示用户作弊风险为低或者无风险。 | 允许用户参加营销活动。 |
| rank2 | 表示用户作弊风险为中。 | 建议给用户营销权益降权或拦截，或者根据客户自身数据做进一步判断。 |
| rank3 | 表示用户作弊风险为高。 | 不允许用户参加营销活动。 |

# 接口调用

## 示例代码

### .js 示例代码
```javascript
// .js
my.ap.preventCheat({
  // 请自行替换 xxxxx 各个参数
  pid: "xxxxxxxxxxxxxxxx",
  bizContext: {
    service: "marketing",
    risk_type: "riskinfo_anticheat_common",
    pid: "xxxxxxxxxxxxxxxx",
    mobile_no: "xxxxxxxxxxx",
    user_id: "xxxxxxxxxxxxxxxxx",
    bank_card_no: "xxxxxxxxxxx",
    client_ip: "null",
    email_address: "null",
    imei: "null",
    imsi: "null",
    mac_address: "null",
    extended_info: "null",
  },
  success(e) {},
});

```

## 入参
Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| pid | String | 是 | 小程序的开放平台账号。 |
| bizContext | Map | 是 | 需要识别的业务参数。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

### Map bizContext
| **属性** | **类型** | **必填** | **最大长度** | **描述** | **示例值** |
| --- | --- | --- | --- | --- | --- |
| service | String | 是 | 128 | 合作伙伴匹配服务类型，固定传 `marketing`，请按照示例值填写。 | 固定传 marketing |
| risk_type | String | 是 | 1024 | 风险策略类型，固定传 `riskinfo_anticheat_common`，请按照示例值填写。 | 固定传 riskinfo_anticheat_common |
| mobile_no | String | 是 | 128 | 用于输入用户注册的手机号码。如果没有获取用户手机号，传入 "null" 即可。 | 13810935692 |
| pid | String | 是 | 128 | 申请业务合作伙伴  ID。 | 20881111222222 |
| user_id | String | 否 | 128 | 支付宝用户 ID。 | 20881111222233 |
| bank_card_no     | String | 否 | 128 | 银行卡号。 | 62223456765456 |
| cert_no | String | 否 | 128 | 用于输入用户的身份证号码。 | 230109199911110921 |
| client_ip | String | 否 | 128 | 账号登录 IP。 | 192.168.0.1 |
| email_address | String | 否 | 128 | 邮箱账号。 | `zhifubao@163.com` |
| imei | String | 否 | 128 | 手机序列号。 | 865736031418584 |
| imsi | String | 否 | 128 | 国际移动用户识别码。 | 460001234567890 |
| mac_address | String | 否 | 128 | MAC 地址或设备唯一标识。 | 42.118.71.72 |
| extended_info | String | 否 | 2048 | 拓展字段，其余信息通过此字段进行传输。<br />业务约定：<ul><li> nickname：账户昵称。</li><li>reg_time：账号注册时间。</li></ul> | "extended_info": { " nickname": "小蚂蚁"," reg_time": "2018-10-01 00:00:09" } |

### Function success
success 回调函数会携带一个 Object 类型的对象，其属性如下：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| result | Object | 风险识别的返回结果。 |

#### Object result
| **属性** | **类型** | **描述** | **示例值** |
| --- | --- | --- | --- |
| riskResult | String | 风险识别结果。<br />>riskinfo_nsf_common 风险评级结果：<ul><li>rank0：提供信息不足，提供参数信息有误，或提供的支付宝账号不存在。</li><li>rank1：表示用户拒付风险为低。</li><li>rank2：表示用户拒付风险为中。</li><li>rank3：表示用户拒付风险为高。</li></ul>riskinfo_anticheat_common_infocode 风险评级说明：171：作弊风险 | {\"riskinfo_anticheat_common\":\"rank3\",\"riskinfo_anticheat_common_infocode\":\"171\"} |
| riskResultDesc | String | 风险信息描述。 | {\"rank0\":\"等级0\"} |
| uniqueId   | String | 业务唯一识别码，用户标识请求信息。 | 0b92uueie87636222 |

### Function fail
fail 回调函数会携带一个 Object 类型的对象，其属性如下：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| error | String | 错误码。 |
| errorMessage | String | 错误信息。 |

## 错误码

| **错误码** | **描述** | **解决方案** |
| --- | --- | --- |
| serviceNoAuth | 服务未授权。 | 请检查配置的账号是否有当前接口权限以及 service 参数是否正确。 |
| riskTypeNoAuth | 场景（risktype）未授权。 | 请检查 risktype 参数是否正确。 |
| bizContentEmpty | 风险数据内容为空。 | 检查入参格式。 |
| paramMissingError | 参数缺失。 | 检查必传参数是否传入。 |
| param error | 参数错误。 | 检查入参格式是否符合文档要求。 |
| SYSTEM_OUT_ERROR | 系统繁忙。 | 请稍后再试。 |
| INVALID_PARAMETER | 缺少必选参数或参数有误。 | 检查参数是否正确或者缺失。 |
| OVER_LIMIT | 超过调用量限制。 | 如需增加额度，请发邮件至 `RiskGoCSC@service.alipay.com` 进行申请。 |
