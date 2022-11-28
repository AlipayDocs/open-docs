# 简介

调用 my.requestSubscribeMessage 后唤起客户端小程序消息订阅界面，回调参数为用户订阅消息的操作结果。订阅前需要在开放平台 **产品绑定** 中先绑定小程序的消息权限，详情可查看 [接入准备](https://opendocs.alipay.com/mini/01rqd3)。

订阅界面是根据当前小程序在 [商家平台](https://mrchportalweb.alipay.com/operation/console/apps) > **运营中心** > 对应小程序详情页 > **消息** > **消息接入** 订阅消息列表中的消息模板 id 来展示对应消息的订阅选项。

其中模版分为一次性订阅模板和长期订阅模板：  
**一次性订阅模板**：每次向用户发送消息都需要用户订阅成功后（次数可累积）才可以发送。用户可以通过勾选 **总是保持以上选择，不再询问** 来默认同意订阅，未勾选的消息会默认拒绝，之后不再弹出订阅面板。  
**长期订阅模板**：用户同意订阅后，可以多次向订阅用户发送消息。用户可点击 **拒绝，不再询问**，来默认拒绝订阅面板所有消息。

用户同意订阅消息成功后，可以通过 [服务端](https://opendocs.alipay.com/mini/02cth2) 向支付宝发送对应模板的消息，然后在支付宝首页、消息盒子、APP PUSH 等位置收到消息提醒。也可以在首次用户授权完成（开发接入完成）之后，通过 [商家平台](https://mrchportalweb.alipay.com/operation/console/apps)> **运营中心** > 对应小程序详情页 > **消息** > **消息接入** 订阅消息列表中的“配置发送”发送消息。

关于消息产品的更多介绍可查看 [消息产品介绍](https://opendocs.alipay.com/mini/introduce/message) 。

# 使用限制
- 一次性模板 id 和长期性模板 id 不可同时使用。
- 开发者调用消息订阅接口，一次性最多传入三个模板 id。
- 基础库 v1.x 从 [1.25.7](https://opendocs.alipay.com/mini/framework/lib) 开始支持，基础库 v2.x 从 [2.7.10](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 开始支持，低版本需要做 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)，使用前可使用 [canIUse](https://opendocs.alipay.com/mini/api/can-i-use) 判断是否支持。
- 基础库版本低于 2.7.15，不能和 web-view 组件共用，会被遮盖。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。


# 效果示例
<img src="https://img.alicdn.com/imgextra/i4/O1CN01apwFaG1lHhVy1z0bc_!!6000000004794-2-tps-762-1530.png" width="300px" height="601px"/>

# 接口调用
## 示例代码
### .js 示例代码

```javascript
my.requestSubscribeMessage({
  entityIds: [
    'ac768fca1ce245ccae9404bb5243c49b',
    '9aa357acb7c6434aba294aded1cdfb7c',
  ],
  success: res => {
    // res.behavior == 'subscribe'
    console.log('接口调用成功的回调', res);
  },
  fail: res => {
    console.log('接口调用失败的回调', res);
  },
  complete: res => {
    console.log('接口调用结束的回调', res);
  },
});
```

## 入参

Object 类型，属性如下：

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| entityIds | Array<String> | 是 | 需要订阅的消息模板id的集合。 |
| thirdTypeAppId | String | 否 | 模板小程序 appid，仅在服务商代调用场景下需要传入。 |
| success | Function | 否 | 订阅成功的回调函数（包括拒绝订阅成功）。 |
| fail | Function | 否 | 订阅失败，或用户取消订阅的回调函数。 |
| complete | Function | 否 | 订阅结束的回调函数（订阅成功、失败、取消都会执行）。 |

## 订阅结束的回调参数

Object 类型，属性如下：

| **属性** | **类型** | **可选值** | **描述** |
| --- | --- | --- | --- |
| behavior | String | 'subscribe', 'cancel', '' | 订阅成功，触发success回调：<br /><ul><li>'subscribe'：表示订阅操作成功（包括拒绝订阅操作）。</ul> 取消订阅操作或订阅失败，触发fail回调：<ul></li><li>'cancel'：表示取消订阅操作。</li><li>''：表示订阅失败</li></ul> |
| keep | Boolean | true, false | 一次订阅模板，用户勾选 **总是保持以上选择，不再询问** 时为 true。 |
| refuse | Boolean | true, false | 长期订阅模板，用户点击 **拒绝，不再询问** 时为 true。 |
| result | Object |  | 订阅数据，<br />{<br />//仅在订阅成功场景下存在，表示订阅成功的模板列表<br />subscribeEntityIds?: [ ],<br />// 最终订阅成功的模板列表<br />subscribedEntityIds: [ ],<br />// 未订阅的模板列表<br />unsubscribedEntityIds: [ ],<br />// 本次新增订阅成功的模板列表<br />currentSubscribedEntityIds: [ ],<br />//仅在取消订阅场景下存在，是传入的模板id集合<br />entityList?: [],<br />}; |
| show | Boolean | true, false | 本次订阅过程是否弹出了订阅面板。 |
| [模板id] | String | 'reject', 'accept' | 动态键，已勾选消息为 ‘accept’，未勾选的消息为 ‘reject’。具体订阅数据建议通过result字段获取。<br/>静默订阅（ show 为 false ）时，返回状态为上一次的订阅结果。 |
| errorCode | Number | 见错误码 | 错误码，仅在订阅取消 / 失败时返回。 |
| errorMessage | String | 见错误码 | 错误信息，仅在订阅取消 / 失败时返回。 |


实际回调参数中error、success、stat已废弃，请使用errorCode、behavior。

## 回调参数示例
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
| 106008 | 模板列表中存在非法/无效的模板 id | 模板 id 传入错误或传入小程序未订购的模板 id。 |
| -1 | 订阅失败/校验模板列表失败 | 默认错误信息。 |

# 常见问题
## Q：调用 my.requestSubscribeMessage 报 “my.requestSubscribeMessage is not afunction”，或 my.canIUse 检测为 false ？
A：先在 IDE 中通过模拟器上方的“展开面板”按钮 -> “设置”查看支持的基础库版本，若不满足此 API 的基础库版本使用限制，可通过升级 IDE 版本来支持更多版本基础库。

## Q：用户对于消息面板的操作，如何实时获取操作结果？
A：1、通过 my.requestSubscribeMessage 回调实时获取；2、用户操作之后，可以通过服务端调用 [alipay.open.app.messagetemplate.subscribe.query](https://opendocs.alipay.com/mini/02cth2) 获取。

## Q：一次性消息模板订阅的消息时选择‘保持以上选择，不再询问’，或长期消息模板确认同意后，订阅消息面板是否还可以再弹出？
A：当用户有以上操作时，若未在小程序胶囊按钮（右上角三个点）中点击 “设置” -> “消息管理” 中切换消息状态，订阅面板将不再弹出，对应的一次性消息模板在切换消息状态后，意味着更改了保持的选择，在下次订阅时面板会再弹出；对应长期模板订阅的消息时，当切换到 “不接收” 时，意味着用户更改了所选消息长期接收的状态，下次订阅时面板会再弹出来。

## Q：如何订阅三个以上消息？
A：目前小程序支持一次订阅消息最多三个，若超过三个，可分多次订阅，分别触发。

## Q：是否还可以使用旧组件 subscribe-msg 订阅消息？
A：my.requestSubscribeMessage 已完全替代 subscribe-msg 订阅消息，建议使用 my.requestSubscribeMessage。

