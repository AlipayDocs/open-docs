# 简介
调起客户端小程序消息订阅界面，返回用户订阅消息的操作结果。详细介绍可查看 [商家消息产品介绍](https://opendocs.alipay.com/mini/introduce/message)。

## 使用限制

- 一次性模板 id 和长期性模板 id 不可同时使用。
- 开发者调用消息订阅接口，一次性最多传入三个模板 id。
- 基础库 v1.x 从 [1.25.7](https://opendocs.alipay.com/mini/framework/lib) 开始支持，基础库 v2.x 从 [2.7.10](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 开始支持，低版本需要做 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)，使用前可使用 [canIUse](https://opendocs.alipay.com/mini/api/can-i-use) 判断是否支持。
- 基础库版本低于 [2.7.15](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2)，不能和 web-view 组件共用，会被遮盖。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码
```javascript
my.requestSubscribeMessage({
  entityIds: ['ac768fca1ce245ccae9404bb5243c49b', '9aa357acb7c6434aba294aded1cdfb7c'],
  success: (res) => {
    // res.behavior == 'subscribe'
    console.log("接口调用成功的回调", res);
  },
  fail: (res) => {
    console.log("接口调用失败的回调", res);
  },
  complete: (res) => {
    console.log("接口调用结束的回调", res);
  }
});
```

## 入参
Object 类型，属性如下：

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| entityIds | Array<String> | 是 | 需要订阅的消息模板的id的集合。 |
| thirdTypeAppId | String | 否 | 模板小程序标识，仅在 ISV 场景下需要传入。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |


## 回调参数
| **属性** | **类型** | **可选值** | **描述** |
| --- | --- | --- | --- |
| behavior | String | '','subscribe','cancel' | 订阅行为。<br /><ul><li>'subscribe'：表示订阅成功。</li><li>'cancel'：表示取消订阅。</li><li>''：表示订阅失败</li></ul> |
| success | Boolean | true, false | 订阅是否成功，已废弃，建议通过 behavior 字段获取订阅状态。 |
| stat | String | 'ok', 'failed' | 订阅状态，已废弃，建议通过 behavior 字段获取订阅状态。 |
| show | Boolean | true, false | 本次订阅过程是否弹出订阅弹层。 |
| result | Object |  | 订阅数据，<br />{<br />//仅在订阅成功场景下存在，表示订阅成功的模板列表<br />subscribeEntityIds?: [ ],<br />// 最终订阅成功的模板列表<br />subscribedEntityIds: [ ],<br />// 未订阅的模板列表<br />unsubscribedEntityIds: [ ],<br />// 本次新增订阅成功的模板列表<br />currentSubscribedEntityIds: [ ],<br />//仅在取消订阅场景下存在，是传入的模板id集合<br />entityList?: [],<br />}; |
| keep | Boolean | true, false | 单次订阅模板，用户同意订阅并勾选 **不再询问** 时为 true。 |
| refuse | Boolean | true, false | 长期订阅模板，用户点击 **拒绝，不再询问** 时为 true。 |
| errorCode | Number | String | 见错误码 | 错误码，仅在订阅取消/失败时返回。 |
| errorMessage | String | 见错误码 | 错误信息，仅在订阅取消/失败时返回。 |
| [模板id] | String | 'reject', 'accept' | 动态键,表示该模板是否被订阅。仅在订阅成功( behavior == 'subscribe' )场景下数据可靠，其他场景下建议通过result字段获取订阅数据。静默订阅（ show 为 false ）时，返回状态为上一次的订阅结果。 |


### 回调参数示例
![消息订阅.jpg](https://cdn.nlark.com/yuque/0/2021/jpeg/179989/1640677925411-8f0cdc4a-9a92-4898-977b-b85fe33e4a89.jpeg#align=left&display=inline&height=2446&margin=%5Bobject%20Object%5D&name=%E6%B6%88%E6%81%AF%E8%AE%A2%E9%98%85.jpg&originHeight=2446&originWidth=3506&size=1158370&status=done&style=none&width=3506)

## 错误码
| **errorCode** | **errorMessage** | **说明** |
| --- | --- | --- |
| 10 | 系统异常 | 系统异常。 |
| 11 | 用户取消订阅 | 用户取消订阅。 |
| 15 | 当前有活跃的订阅授权窗口，此次调用不会弹窗，无订阅结果返回 | 重复触发消息订阅，调用失败。 |
| 203 | 无效的参数 | 传入参数错误，比如传入模板 id 数量大于 3。 |
| 402 | 应用暂不能提供服务 | 传入错误的小程序 APPID。 |
| 100201 | 调用次数超限 | 接口限流。 |
| 106002 | 模板列表中同时存在一次性/长期订阅模板 | 模板列表中不能同时存在一次性/长期订阅模板。 |
| 106008 | 模板列表中存在非法/无效的模板id | 模板 id 传入错误或传入小程序未订购的模板 id。 |
| -1 | 订阅失败/校验模板列表失败 | 默认错误信息。 |
