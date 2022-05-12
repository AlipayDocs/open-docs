# 简介
**my.ap.imgRisk** 是图片风险任务提交接口，用于识别图片是否有色情、违禁违法等内容。

有关图片内容安全的产品和接入介绍，可查看 [图片内容安全](https://opendocs.alipay.com/mini/introduce/img_risk)。

## 使用限制

- 基础库 [1.14.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.60 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此接口为异步请求接口，首先需要发起风险识别请求，获取任务 ID。等待 500 毫秒（ms）后再通过任务 ID 请求结果。
- 此 API 暂仅支持企业支付宝小程序使用。

### 1. 调用参数说明

- 通过传输图片内容判断此图片信息中是否包含风险信息，图片需要传输 URL。
- 图片必须是公网可以访问的图片，如果有加密或者限权，则无法返回结果。

### 2. 返回参数说明

- REJECTED：拒绝，代表此图片风险程度高，不能发布展示。
- PASSED：通过，代表此图片的风险程度低，可以发布展示。

### 3. 图片风险任务提交

# 接口调用

## 示例代码

### .js 示例代码
```javascript
// .js
my.ap.imgRisk({
  pid:'xxxxxxxxxxxxxxxx',  
  bizContext: {
    'risk_type': 'img_risk',
    content: 'http://www.xxxxxx.com.cn//xxxxxx/xxxxxxx/images/xxxx/xx/xxx.png'
  },
  success(e) {
  },
})
```

## 入参
Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| pid | String | 是 | 合作者身份 ID。即商家与支付宝签约后，商家获得的支付宝商家唯一识别码。 |
| bizContext | Object | 是 | 需要识别的业务参数。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

### Object bizContext
| **属性** | **类型** | **必填** | **最大长度** | **描述** | **示例值** |
| --- | --- | --- | --- | --- | --- |
| risk_type | String | 是 | 1024 | 风险类型。 | 固定传 img_risk |
| content | String | 是 | 128 | 需要验证的图片 URL。 | [https://ss1.bdstatic.com/70cFvXSh_Q1YnxGkpoWK1HF6hhy/it/u=3180559933,1841450308&fm=26&gp=0.jpg](https://ss1.bdstatic.com/70cFvXSh_Q1YnxGkpoWK1HF6hhy/it/u=3180559933,1841450308&fm=26&gp=0.jpg) |

### Function success
success 回调函数会携带一个 Object 类型的对象，其属性如下：

| **属性** | **类型** | **最大长度** | **描述** | **示例值** |
| --- | --- | --- | --- | --- |
| riskResult      | String | 128 | 图片风险识别的任务的任务ID。 | \"apply_id\":\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\ |
| riskResultDesc | String | 1024 | 风险识别结果描述。 | 返回结果会默认为空，忽略即可 |
| success | Boolean | - | 是否调用成功。 | true |
| uniqueId | String | 1024 | 业务唯一识别码。 | xxxxxxxxxxxxxxxxx |

### Function fail
fail 回调函数会携带一个 Object 类型的对象，其属性如下：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| errorCode | String | 错误码。 |
| errorMessage | String | 错误信息。 |
