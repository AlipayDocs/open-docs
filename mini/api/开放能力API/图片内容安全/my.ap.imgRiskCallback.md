# 简介

**my.ap.imgRiskCallback** 是用于查询图片的风险识别结果的 API。

有关图片内容安全的产品和接入介绍，可查看 [图片内容安全](https://opendocs.alipay.com/mini/introduce/img_risk)。

## 使用限制

- 基础库 [1.14.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.60 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 暂仅支持企业支付宝小程序使用。

## 接口说明

此接口为异步请求接口。首先需要通过 [my.ap.imgRisk](https://opendocs.alipay.com/mini/api/img_risk) 发起风险识别请求，获取任务 ID；等待 500 毫秒后再使用本接口，传递任务 ID 请求最终结果。

# 接口调用

## 示例代码

### .js 示例代码

```javascript
// .js
my.ap.imgRiskCallback({
  pid: 'xxxxxxxxxxxxxxxx', // 替换成您的 pid
  bizContext: {
    risk_type: 'img_risk_result',
    apply_id: 'xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx',
  },
  success(e) {},
});
```

### 1. 调用参数说明

- 通过传输图片内容判断此图片信息中是否包含风险信息，图片需要传输 URL。
- 图片必须是公网可以访问的图片，如果有加密或者限权，则无法返回结果。

### 2. 返回参数说明

- REJECTED：拒绝，代表此图片风险程度高，不能发布展示。
- PASSED：通过，代表此图片的风险程度低，可以发布展示。

## 入参

Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| pid | String | 是 | 小程序的开放平台账号。 |
| bizContext | Object | 是 | 需要识别的业务参数。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

### Object bizContext

| **参数** | **类型** | **必填** | **最大长度** | **描述** | **示例值** |
| --- | --- | --- | --- | --- | --- |
| risk_type | String | 是 | 1024 | 风险类型。 | 固定传 img_risk_result |
| apply_id | String | 是 | 128 | 需要查询图片的任务 ID。 | 2eee1a72-4f32-45d6-bfa3-0f7173cde80b |

### Function success

success 回调函数会携带一个 Object 类型的对象，其属性如下：

| **参数** | **类型** | **最大长度** | **描述** | **示例值** |
| --- | --- | --- | --- | --- |
| riskResult | String | 128 | 图片风险识别的任务的任务 ID。 | \"action\":\"REJECTED\"<br /> <br />\"action\":\"PASSED\" |
| riskResultDesc | String | 1024 | 风险识别结果描述。 | \"REJECTED\":\"拦截\"<br /> <br />\"PASSED\":\"放过\" |
| success | Boolean | - | 是否调用成功。 | true |
| uniqueId | String | 1024 | 业务唯一识别码 | 0b92uueie87636222 |

### Function fail

fail 回调函数会携带一个 Object 类型的对象，其属性如下：

| **属性**     | **类型** | **描述**   |
| ------------ | -------- | ---------- |
| errorCode    | String   | 错误码。   |
| errorMessage | String   | 错误信息。 |

## 错误码

| **错误码** | **说明** | **解决方案** |
| --- | --- | --- |
| serviceNoAuth | 服务未授权。 | 请检查配置的账号是否已签约响应的功能包。 |
| riskTypeNoAuth | 场景（risktype）未授权。 | 请检查配置的账号是否已签约响应的功能包，<br />请检查 risktype 参数是否正确。 |
| bizContentEmpty | 风险数据内容为空。 | 检查入参数据格式。 |
| paramMissingError | 参数缺失。 | 检查必传参数是否传入。 |
| param error | 参数错误。 | 检查入参格式是否符合文档要求。 |
| SYSTEM_OUT_ERROR | 系统繁忙。 | 请稍后再试。 |
| INVALID_PARAMETER | 缺少必选参数或参数有误。 | 检查参数是否正确或者缺失。 |
| OVER_LIMIT | 超过调用量限制。 | 如需增加额度，请发邮件至 `RiskGoCSC@service.alipay.com` 进行申请。 |

## FAQ

### 1、没有返回识别结果该如何处理?

确认风险识别的任务 ID，为此图片对应的任务 ID。

500 ms 后若返回空，建议等待 500 ms 后重试。一共重试 3 次，若全为空，尝试重新提交审核任务。

### 2、图片说明格式以及大小？

- 图片格式支持：BMP, PNG, JPEG, TIFF, SVG, ICO。
- 图片大小：0~10 MB。
- 图片的 URL 需要可访问。如果出现无法访问，下载失败，非图片格式会返回通过。

### 3、调用频率是怎样的？

该接口暂不推荐并发调用。
