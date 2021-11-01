
# 简介
本文概述了小程序开放能力涉及的服务端 API 及其作用，更多接口使用详情参见 [开放能力](https://opendocs.alipay.com/mini/00am3f)。

**说明：**

- 更多接口文档参见 [API](https://opendocs.alipay.com/apis)。
- 服务端 SDK 使用前，请下载 [开发工具包（SDK）](https://opendocs.alipay.com/open/54/cyz7do#%E6%9C%8D%E5%8A%A1%E7%AB%AF%20SDK)。

# 基础能力

## 小程序二维码
| 接口英文名 | 接口中文名 | 接口描述 |
| --- | --- | --- |
| [alipay.open.app.qrcode.create](https://opendocs.alipay.com/mini/api/openapi-qrcode) | 小程序生成推广二维码接口 | 生成小程序推广二维码。 |


## 用户授权
| 接口英文名 | 接口中文名 | 接口描述 |
| --- | --- | --- |
| [alipay.system.oauth.token](https://docs.open.alipay.com/api_9/alipay.system.oauth.token) | 换取授权访问令牌 | 换取授权访问令牌。 |


## 小程序订单中心
| 接口英文名 | 接口中文名 | 接口描述 |
| --- | --- | --- |
| [alipay.open.auth.token.app](https://docs.open.alipay.com/api_9/alipay.open.auth.token.app) | 换取应用授权令牌 | 在应用授权的场景下，商户把名下应用授权给 ISV 后，支付宝会给 ISV 颁发应用授权码app_auth_code，ISV 可通过获取到的 app_auth_code 换取 app_auth_token。 <br />后续 ISV 需传入 app_auth_token 代商家调用接口。 |
| [alipay.merchant.item.file.upload](https://docs.open.alipay.com/api_4/alipay.merchant.item.file.upload) | 商品图片上传接口 | 商户把商品对应的图片文件上传到支付宝，后续通过该接口返回的素材 ID 及素材 key 创建商品或展示商品图片。 |
| [alipay.merchant.order.sync](https://docs.open.alipay.com/api_4/alipay.merchant.order.sync) | 订单数据同步接口 | 商户可以调用此接口同步对应订单数据至小程序订单中心。 |
| [ant.merchant.expand.item.open.create](https://docs.open.alipay.com/api_4/ant.merchant.expand.item.open.create/) | 创建商品接口 | 用于 ISV 或商户创建商品。 |
| [ant.merchant.expand.item.open.modify](https://docs.open.alipay.com/api_4/ant.merchant.expand.item.open.modify/) | 修改商品接口 | 用于 ISV 或商户修改商品。 |
| [ant.merchant.expand.item.open.query](https://docs.open.alipay.com/api_4/ant.merchant.expand.item.open.query) | 查询商品接口 | 用于 ISV 或商户查询商品。 |
| [ant.merchant.expand.item.open.batchquery](https://docs.open.alipay.com/api_4/ant.merchant.expand.item.open.batchquery) | 批量查询商品接口 | 用于 ISV 或商户批量查询商品。 |
| [ant.merchant.expand.item.open.delete](https://docs.open.alipay.com/api_4/ant.merchant.expand.item.open.delete) | 删除商品接口 | 用于 ISV 或商户删除商品。 |


## 小程序内容同步
| 接口英文名 | 接口中文名 | 接口描述 |
| --- | --- | --- |
| [alipay.open.mini.content.sync](https://opendocs.alipay.com/apis/00wik8)﻿ | 小程序内容接入 | 支持小程序同步小程序服务、商品信息接入、门店绑定内容类型。 |
| [alipay.open.app.appcontent.function.create](https://opendocs.alipay.com/apis/011agl) | [](https://opendocs.alipay.com/apis/011agl)小程序服务创建 | 创建小程序服务，获取小程序服务 code。 |
| [alipay.open.app.appcontent.function.query](https://opendocs.alipay.com/apis/0119at) | [](https://opendocs.alipay.com/apis/0119at) [](https://opendocs.alipay.com/apis/011bkt)小程序服务查询 | 查询小程序服务的审核状态。 |
| [alipay.open.app.appcontent.function.modify](https://opendocs.alipay.com/apis/011bks) | [](https://opendocs.alipay.com/apis/011bks)小程序服务编辑 | 小程序服务被驳回需要重新提审或修改服务基础信息时，可以通过接口来编辑服务并提交审核。 |
| [alipay.open.app.appcontent.function.offline](https://opendocs.alipay.com/apis/011bkt) | [](https://opendocs.alipay.com/apis/011bkt)小程序服务失效 | 当小程序服务需要删除时，可以通过接口来删除服务。服务被删除后，该服务无法再在 C 端被曝光。 |


## 蚂蚁门店管理
| 接口英文名 | 接口中文名 | 接口描述 |
| --- | --- | --- |
| [ant.merchant.expand.shop.query](https://opendocs.alipay.com/apis/014yih) | 店铺查询接口 | 用于查询对应账号下拥有支付宝门店信息。 |
| [ant.merchant.expand.shop.save.passed](https://opendocs.alipay.com/apis/014ouh) | 店铺审核通过消息 | 创建蚂蚁门店接口中创建商户审核通过后，支付宝通过本接口推送成功消息至应用网关。 |
| [ant.merchant.expand.shop.create](https://opendocs.alipay.com/apis/014tmc) | 蚂蚁店铺创建 | 创建蚂蚁门店（即支付宝门店）。 |
| [ant.merchant.expand.shop.modify](https://opendocs.alipay.com/apis/014tmb) | 修改蚂蚁店铺 | 修改蚂蚁门店信息，按信息项修改。若无特殊说明，如果某项存在但是没填写，则不会覆盖掉原来的值。 |
| [ant.merchant.expand.order.query](https://opendocs.alipay.com/apis/014oug) | 商户申请单查询 | 开发者可根据申请单 ID，查询自己提交的商户进件、管理等申请单。 |
| [ant.merchant.expand.shop.close](https://opendocs.alipay.com/apis/014slp) | 蚂蚁店铺关闭 | 通过 shop_id 关闭蚂蚁门店。 |
| [ant.merchant.expand.shop.save.rejected](https://opendocs.alipay.com/apis/014slo) | 店铺审核拒绝通过消息 | 创建蚂蚁门店接口中创建商户审核失败后，支付宝通过本接口推送审核失败消息至应用网关。 |
| [ant.merchant.expand.indirect.image.upload](https://opendocs.alipay.com/apis/013lfq) | 图片上传 | 图片资料上传。 |


# 支付能力

## 小程序支付
| 接口英文名 | 接口中文名 | 接口描述 |
| --- | --- | --- |
| [alipay.trade.create](https://docs.open.alipay.com/api_1/alipay.trade.create/) | 统一收单交易创建接口 | 商户通过该接口进行交易的创建下单。 |
| [alipay.open.agent.facetoface.sign](https://docs.open.alipay.com/api_50/alipay.open.agent.facetoface.sign/) | 代签约当面付接口（也适用于服务商代替商户签约小程序支付） | 三方应用代理签约当面付产品，需要配合开启事务接口使用。 |


# 资金能力

## 周期扣款

### 签约接口
| 接口英文名 | 接口中文名 | 接口描述 |
| --- | --- | --- |
| [alipay.user.agreement.page.sign](https://docs.open.alipay.com/api_2/alipay.user.agreement.page.sign) | 支付宝个人协议页面签约接口 | 开发者可通过该接口传入周期扣款协议相关限制内容，生成签约参数用于小程序唤起签约页面。<br />目前支持支付宝钱包 H5 页面签约、扫码签约等方式。 |
| [alipay.user.agreement.query](https://docs.open.alipay.com/api_2/alipay.user.agreement.query) | 支付宝个人代扣协议查询接口 | 支付宝个人代扣协议查询接口，通过该接口可查询用户协议信息。  |
| [alipay.user.agreement.unsign](https://docs.open.alipay.com/api_2/alipay.user.agreement.unsign) | 支付宝个人代扣协议解约接口 | 支付宝个人代扣协议解约接口，通过该接口可解除用户在约协议。 |
| [alipay.user.agreement.executionplan.modify](https://docs.open.alipay.com/api_2/alipay.user.agreement.executionplan.modify) | 周期性扣款协议执行计划修改接口 | 通过该接口，商户可以实现延期扣款。 |
| [alipay.user.agreement.transfer](https://docs.open.alipay.com/api_2/alipay.user.agreement.transfer) | 协议由普通通用代扣协议产品转移到周期扣协议产品 | 商户通过接口将普通通用的代扣协议转移成周期扣款协议。 |


### 支付接口
| 接口英文名 | 接口中文名 | 接口描述 |
| --- | --- | --- |
| [alipay.trade.pay](https://docs.open.alipay.com/api_1/alipay.trade.pay/) | 统一收单交易支付接口 | 用户在完成协议签约后，商户可通过本接口完成协议规定的后续代扣。 |
| [alipay.trade.app.pay](https://docs.open.alipay.com/api_1/alipay.trade.app.pay) | APP 支付 2.0 接口 | 外部商户 APP 唤起快捷 SDK 创建订单并支付。 |
| [alipay.trade.refund](https://docs.open.alipay.com/api_1/alipay.trade.refund/) | [](https://docs.open.alipay.com/api_1/alipay.trade.refund/)统一收单交易退款接口 | 当交易发生之后一段时间内，卖家可以通过退款接口将支付款退还给买家，支付宝按照退款规则将支付款按原路退到买家帐号上。 |
| [alipay.trade.query](https://docs.open.alipay.com/api_1/alipay.trade.query/) | [](https://docs.open.alipay.com/api_1/alipay.trade.query/)统一收单线下交易查询 | 该接口提供所有支付宝支付订单的查询，商户可以通过该接口主动查询支付订单状态，完成下一步的业务逻辑。 |
| [alipay.trade.cancel](https://docs.open.alipay.com/api_1/alipay.trade.cancel/) | [](https://docs.open.alipay.com/api_1/alipay.trade.cancel/)统一收单交易撤销接口 | 支付交易返回失败或支付系统超时，调用该接口撤销交易。 |
| [alipay.trade.close](https://docs.open.alipay.com/api_1/alipay.trade.close/) | [](https://docs.open.alipay.com/api_1/alipay.trade.close/)统一收单交易关闭接口 | 用于交易创建后，用户在一定时间内未进行支付，可调用该接口直接将未付款的交易进行关闭。 |


## 商家分账

### 分账关系维护
| 接口英文名 | 接口中文名 | 接口描述 |
| --- | --- | --- |
| [alipay.trade.royalty.relation.bind](https://docs.open.alipay.com/api_31/alipay.trade.royalty.relation.bind) | 分账关系绑定 | 开发者可通过该接口批量维护商家与分账方关系，批量进行分账关系绑定。 |
| [alipay.trade.royalty.relation.unbind](https://docs.open.alipay.com/api_31/alipay.trade.royalty.relation.unbind) | 分账关系解绑 | 开发者可通过该接口批量维护商家与分账方关系，批量进行分账关系解绑。 |
| [alipay.trade.royalty.relation.batchquery](https://docs.open.alipay.com/api_31/alipay.trade.royalty.relation.batchquery) | 分账关系查询 | 开发者可通过该接口批量维护商家与分账方关系，分页查询分账关系。 |


### 分账请求接口
| 接口英文名 | 接口中文名 | 接口描述 |
| --- | --- | --- |
| [alipay.trade.order.settle](https://docs.open.alipay.com/api_1/alipay.trade.order.settle) | 统一收单交易结算接口 | 用于在线下场景交易支付后，进行卖家与第三方（如供应商或平台商）基于交易金额的分佣结算。 |


### 分账查询接口
| 接口英文名 | 接口中文名 | 接口描述 |
| --- | --- | --- |
| [alipay.trade.query](https://docs.open.alipay.com/api_1/alipay.trade.query) | 统一收单线下交易查询接口 | 用于卖家与第三方（如供应商或平台商）基于交易金额的已分佣明细查询。通过传递 "query_options":["TRADE_SETTE_INFO"] 参数查询分账明细。 |


### 退款退分账接口
| 接口英文名 | 接口中文名 | 接口描述 |
| --- | --- | --- |
| [alipay.trade.refund](https://docs.open.alipay.com/api_1/alipay.trade.refund/) | 统一收单交易退款接口 | 用于卖家与第三方（如供应商或平台商）基于交易金额的退分佣信息。<br />通过 refund_royalty_parameters 传递退分佣信息。 |


## 转账到支付宝账户
| 接口英文名 | 接口中文名 | 接口描述 |
| --- | --- | --- |
| [alipay.fund.trans.uni.transfer](https://docs.open.alipay.com/api_28/alipay.fund.trans.uni.transfer) | 用于向指定支付宝账户转账 | 单笔转账接口是基于支付宝的资金处理能力，提供通过 API 接口完成企业自身支付宝账户到支付宝账户、企业自身支付宝账户到银行卡的转账功能。 |
| [alipay.fund.trans.common.query](https://docs.open.alipay.com/api_28/alipay.fund.trans.common.query/) | 用于查询转账结果 | 商户可通过该接口查询转账业务单据的状态。 |
| [alipay.fund.account.query](https://docs.open.alipay.com/api_28/alipay.fund.account.query) | 用于查询支付宝账户余额 | 可查询请求方的支付宝账户余额信息。 |
| [alipay.fund.trans.order.changed](https://docs.open.alipay.com/msgapi_60/alipay.fund.trans.order.changed) | 用于转账单据状态变更后触发的通知 | 单笔转账到支付宝账户、单笔转账到银行卡、C2C 现金红包、B2C 现金红包单据状态变更后触发的通知。 |


## 资金预授权
| 接口英文名 | 接口中文名 | 接口描述 |
| --- | --- | --- |
| [alipay.fund.auth.order.app.freeze](https://docs.open.alipay.com/api_28/alipay.fund.auth.order.app.freeze) | 线上资金授权冻结接口 | 创建支付宝授权订单并完成资金冻结。适用于线上场景完成资金授权，例如从商户 APP 端拉起支付宝收银台完成冻结。 |
| [alipay.fund.auth.order.unfreeze](https://docs.open.alipay.com/api_28/alipay.fund.auth.order.unfreeze) | 资金授权解冻接口 | 商家可将需要解冻的授权资金通过该接口进行解冻。支付宝在收到解冻请求并验证成功后，依循解冻规则将冻结资金按原路解冻。 |
| [alipay.fund.auth.operation.cancel](https://docs.open.alipay.com/api_28/alipay.fund.auth.operation.cancel) | 资金授权撤销接口 | 只有商户由于业务系统处理超时需要终止后续业务处理或者授权结果未知时可调用撤销，其他正常授权冻结的操作如需实现相同功能请调用 资金授权解冻接口。<br />提交资金授权后调用 资金授权操作查询，没有明确的授权结果再调用 资金授权撤销。 |
| [alipay.fund.auth.operation.detail.query](https://docs.open.alipay.com/api_28/alipay.fund.auth.operation.detail.query) | 资金授权操作查询接口 | 通过该接口可以查询单笔明细的详细信息。 |
| [alipay.trade.pay](https://docs.open.alipay.com/api_1/alipay.trade.pay/) | 统一收单交易支付接口 | 用户在完成协议签约后，商户将用户签约协议号通过本接口送至支付宝完成代扣支付。 |
| [alipay.trade.query](https://docs.open.alipay.com/api_1/alipay.trade.query/) | 统一收单线下交易查询 | 该接口提供所有支付宝支付订单的查询，商户可以通过该接口主动查询订单状态，完成下一步的业务逻辑。 |
| [alipay.trade.refund](https://docs.open.alipay.com/api_1/alipay.trade.refund) | 统一收单交易退款接口 | 当交易发生之后一段时间内，卖家可以通过退款接口将支付款退还给买家，支付宝按照退款规则将支付款按原路退到买家帐号上。 |
| [alipay.trade.orderinfo.sync](https://docs.open.alipay.com/api_1/alipay.trade.orderinfo.sync) | 支付宝订单信息同步接口 | 该接口用于商户向支付宝同步该笔订单相关业务信息。 |
| [alipay.data.dataservice.bill.downloadurl.query](https://docs.open.alipay.com/api_15/alipay.data.dataservice.bill.downloadurl.query) | 查询对账单下载地址 | 为方便商户快速查账，支持商户通过本接口获取商户离线账单下载地址。 |


# 会员能力

## 商户会员卡

### 基础接口
| 接口英文名 | 接口中文名 | 接口描述 |
| --- | --- | --- |
| [alipay.offline.material.image.upload](https://docs.open.alipay.com/api_3/alipay.offline.material.image.upload) | 图片资料上传 | 开发者需先将要使用的图片上传至支付宝服务器，获取对应的图片 ID 用于后续配置会员卡模板等接口。 |


### 会员卡模板管理
| 接口英文名 | 接口中文名 | 接口描述 |
| --- | --- | --- |
| [alipay.marketing.card.template.create](https://docs.open.alipay.com/api_5/alipay.marketing.card.template.create) | 会员卡模板创建 | 会员卡模板创建。 |
| [alipay.marketing.card.template.modify](https://docs.open.alipay.com/api_5/alipay.marketing.card.template.modify) | 会员卡模板修改 | 开发者可调用该接口修改制定会员卡模板。<br />注意：<br />1.修改会员卡模板后，该模板下所有会员卡都会更新（ 包括已发放会员卡）。<br />2.修改会员卡模板，field_rule_list（字段规则列表）配置项不支持修改，设置后无效。<br />3.会员卡设置 shop_ids 后，shop_ids 只支持新增或修改门店，但是不支持删除 shop_ids 参数。<br />4.其他修改项因为线上缓存的缘故，模板更新可能存在 1-5 分钟延时。|
| [alipay.marketing.card.template.query](https://docs.open.alipay.com/api_5/alipay.marketing.card.template.query) | 会员卡模板查询接口 | 会员卡模板查询接口。 |


### 开卡组件
| 接口英文名 | 接口中文名 | 接口描述 |
| --- | --- | --- |
| [alipay.marketing.card.formtemplate.set](https://docs.open.alipay.com/api_5/alipay.marketing.card.formtemplate.set) | 会员卡开卡表单模板配置 | 开发者可通过本接口配置用户开卡时需提交信息。 |
| [alipay.marketing.card.activateurl.apply](https://docs.open.alipay.com/api_5/alipay.marketing.card.activateurl.apply) | 获取会员卡领卡投放链接 | 会员卡开卡业务，开发者通过该接口获取用户开卡链接，用于会员卡投放。<br />小程序场景中无需传入 callback 地址。 |
| [alipay.marketing.card.activateform.query](https://docs.open.alipay.com/api_5/alipay.marketing.card.activateform.query) | 查询用户提交的会员卡表单信息 | 会员卡开卡场景下，用户确认领卡后，跳转到商户开卡处理页面，商户通过该接口查询用户表单信息。 |


### 会员卡管理
| 接口英文名 | 接口中文名 | 接口描述 |
| --- | --- | --- |
| [alipay.marketing.card.open](https://docs.open.alipay.com/api_5/alipay.marketing.card.open) | 会员卡开卡 | 开发者可调用本接口给用户开卡，成功后会员卡将自动添加至用户卡包。 |
| [alipay.marketing.card.update](https://docs.open.alipay.com/api_5/alipay.marketing.card.update) | 会员卡更新 | 开发者可调用本接口更新用户开取的某张会员卡信息，如积分等。<br />注意：<br />1.更新会员卡后，只有该张会员卡会进行更新，其他会员卡不会更新。<br />2.open_date（开卡时间）和 valid_date（结束时间）不支持修改，设置后无效。<br />3.不支持设置 notify_messages（卡信息变更通知消息），设置后无效，不会发送通知。<br />4.其他修改项因为线上缓存的缘故，模板更新可能存在 1-5 分钟延时。|
| [alipay.marketing.card.delete](https://docs.open.alipay.com/api_5/alipay.marketing.card.delete) | 会员卡删卡 | 开发者可通过本接口删除用户开取的会员卡。 |
| [alipay.marketing.card.query](https://docs.open.alipay.com/api_5/alipay.marketing.card.query) | 会员卡查询 | 根据卡号或者持卡人信息查询用户在开卡页面提交的信息。 |


## 支付宝身份验证
| 接口英文名 | 接口中文名 | 接口描述 |
| --- | --- | --- |
| [alipay.user.certify.open.query](https://docs.open.alipay.com/api_2/alipay.user.certify.open.query) | 身份认证记录查询 | 商户在开放认证完成后，调用本接口查询认证状态和相关数据。 |
| [alipay.user.certify.open.initialize](https://docs.open.alipay.com/api_2/alipay.user.certify.open.initialize) | 身份认证初始化服务 | 开发者可调用本接口，传入用户实名信息初始化支付宝开放认证服务，创建开放认证流程并获取 certify_id。 |
| [alipay.user.certify.open.certify](https://docs.open.alipay.com/api_2/alipay.user.certify.open.certify) | 身份认证开始认证 | 在完成开放认证初始化后，开发者可调用本接口开始认证流程，获取身份验证链接用于小程序跳转至身份验证页。 |


# 营销能力

## 支付宝卡包
| 接口英文名 | 接口中文名 | 接口描述 |
| --- | --- | --- |
| [alipay.pass.template.add](https://opendocs.alipay.com/apis/api_24/alipay.pass.template.add) | 卡券模板创建接口 | 创建卡券的模板，卡券的样式、内容信息通过该接口提交到支付宝，支付宝会生成模板 ID 反馈给开发者，用于后续的更新和发放。 |
| [alipay.pass.template.update](https://opendocs.alipay.com/apis/api_24/alipay.pass.template.update) | 卡券模板更新接口 | <br />对于已经创建的模板，如果需要修改模板内容，可通过该接口修改，适用于修改模板内容。<br />对于已经发布的模板，如果需要修改内容并同步到用户端，则应使用 卡券实例更新接口。|
| [alipay.pass.instance.add](https://opendocs.alipay.com/apis/api_24/alipay.pass.instance.add) | 卡券实例发放接口 | 卡券模板生成后，如需将卡券发布给对应的用户，则调用此接口。 |
| [alipay.pass.instance.update](https://opendocs.alipay.com/apis/api_24/alipay.pass.instance.update) | 卡券实例更新接口 | 对于已经发布的卡券，如需更新内容，可通过此接口更新，主要用于更新卡券的使用状态。 |
| [alipay.user.pass.instancebatch.add](https://opendocs.alipay.com/apis/009z8j) | 卡券实例批量发放接口 | 商家向用户一次性发放多张卡券时使用，常被称作优惠大礼包。支付宝将保证批次的事务型，即全部发放成功或全部发放失败。 |


## 现金红包
| 接口英文名 | 接口中文名 | 接口描述 |
| --- | --- | --- |
| [alipay.fund.trans.uni.transfer](https://docs.open.alipay.com/api_28/alipay.fund.trans.uni.transfer) | 统一转账接口 | 单笔转账接口是基于支付宝的资金处理能力，提供通过 API 接口完成企业自身支付宝账户到支付宝账户、企业自身支付宝账户到银行卡的转账功能。 |
| [alipay.fund.trans.common.query](https://docs.open.alipay.com/api_28/alipay.fund.trans.common.query/) | 单据查询接口 | 商户可通过该接口查询转账业务单据的状态。 |
| [alipay.fund.trans.order.changed](https://docs.open.alipay.com/msgapi_60/alipay.fund.trans.order.changed) | 单据状态变更后触发的通知接口 | 单笔转账到支付宝账户、单笔转账到银行卡、C2C 现金红包、B2C 现金红包单据状态变更后触发的通知。 |


## 无资金商户优惠券
| 接口英文名 | 接口中文名 | 接口描述 |
| --- | --- | --- |
| [alipay.marketing.cashlessvoucher.template.create](https://docs.open.alipay.com/api_5/alipay.marketing.cashlessvoucher.template.create) | 无资金券模板创建接口 | 创建无资金全场优惠券模板。<br />- 全场优惠券暂时只支持"无资金代金券"(CASHLESS_FIX_VOUCHER)。|
| [alipay.marketing.cashlessvoucher.template.modify](https://docs.open.alipay.com/api_5/alipay.marketing.cashlessvoucher.template.modify) | 无资金券模板修改接口 | 修改无资金券模板。 |
| [alipay.marketing.voucher.send](https://docs.open.alipay.com/api_5/alipay.marketing.voucher.send) | 发券接口 | 开发者可调用本接口通过用户 user_id 向用户发券。 |
| [alipay.marketing.voucher.templatedetail.query](https://docs.open.alipay.com/api_5/alipay.marketing.voucher.templatedetail.query) | 查询模板详情 | 查询模板的详细信息，包含准实时的汇总信息。 |
| [alipay.marketing.voucher.templatelist.query](https://docs.open.alipay.com/api_5/alipay.marketing.voucher.templatelist.query) | 查询券模板列表 | 分页查询当前 PID 下的所有模板。 |
| [alipay.marketing.voucher.query](https://docs.open.alipay.com/api_5/alipay.marketing.voucher.query) | 券查询 | 商户券信息查询。 |
| [alipay.marketing.userule.pid.query](https://docs.open.alipay.com/api_5/alipay.marketing.userule.pid.query) | 商户使用场景规则PID查询 | 查询商户可用于使用场景规则的 PID。 |
| [ant.merchant.expand.merchant.storelist.query](https://docs.open.alipay.com/api_3/ant.merchant.expand.merchant.storelist.query) | 商户外部门店查询接口 | 查询商户外部门店。 |
| [alipay.marketing.material.image.upload](https://opendocs.alipay.com/pre-apis/00a8ae) | 营销图片上传接口 | 开发者可调用本接口上传单品优惠券模板中使用的商品图片，获取图片 id。 |
| [alipay.marketing.cashlessitemvoucher.template.create](https://opendocs.alipay.com/pre-apis/00a8ip) | 无资金单品券创建接口 | 开发者可调用本接口创建无资金单品优惠券模板。 |


## 模板消息
| 接口英文名 | 接口中文名 | 接口描述 |
| --- | --- | --- |
| [alipay.open.app.mini.templatemessage.send](https://opendocs.alipay.com/apis/009zv5) | 小程序发送模板消息 | 小程序通过 OpenAPI 给用户触达消息，主要为支付后的触达（通过支付宝订单号 trade_no）、用户提交表单后的触达（通过 formId）。 |


# 安全能力

## e签宝电子合同

### 合同模板相关接口
| 接口英文名 | 接口中文名 | 接口描述 |
| --- | --- | --- |
| [alipay.eco.doc.template.create](https://opendocs.alipay.com/apis/00jr6o) | 创建合同模板 | 调用接口创建合同模板，通过获取到的 uploadUrl 进行文件流上传 Word/PDF 文件，文件上传后模板才可使用。 |
| [alipay.eco.doctemplate.settingurl.query](https://opendocs.alipay.com/apis/00jr6p) | 获取合同模板设置地址 | 调用接口获取已经创建并上传文件的合同模板设置页面地址。 |


### 合同签署相关接口
| 接口英文名 | 接口中文名 | 接口描述 |
| --- | --- | --- |
| [alipay.eco.contract.signflows.create](https://opendocs.alipay.com/apis/00prvn) | 创建签署流程 | 基于合同模板创建合同签署流程。调用此接口前，需完成模版创建及组件设置。 |
| [alipay.eco.sign.flow.query](https://opendocs.alipay.com/apis/api_50/alipay.eco.sign.flow.query) | 签署流程查询 | 可通过此接口查询流程、签署人的签署状态。 |
| [alipay.eco.signflows.url.query](https://opendocs.alipay.com/apis/00pvbe) | 获取流程签署地址 | 创建签署流程后，可通过此接口获取指定签署人的签署链接。 |
| [alipay.eco.signflows.detail.query](https://opendocs.alipay.com/apis/api_50/alipay.eco.signflows.detail.query) | 流程文档下载 | 可通过此接口获取签署流程合同与附件的下载地址。 |
| [alipay.eco.file.path.query](https://opendocs.alipay.com/apis/api_50/alipay.eco.file.path.query) | 获取文件直传地址 | 通过获取到的 uploadUrl 进行文件流上传合同的附件，如订单截图等，可作为电子合同的辅助证明材料。上传文件具体注意事项参见 [文件流上传方法](https://opendocs.alipay.com/mini/00kr2w)。 |
| [alipay.eco.sign.flow.cancel](https://opendocs.alipay.com/apis/api_50/alipay.eco.sign.flow.cancel) | 签署流程撤销 | 可通过此接口撤销合同签署流程。场景举例：用户取消订单后，需通过流程ID（flow_id）撤销对应的电子合同签署流程。 |


## 文本风险识别
| 接口英文名 | 接口中文名 | 接口描述 |
| --- | --- | --- |
| [alipay.security.risk.content.detect](https://docs.open.alipay.com/api_49/alipay.security.risk.content.detect) | 文本风险识别（服务端） | 蚁盾为小程序提供的用于内容风险检测的服务，适用范围仅限于正在使用小程序的商户。 |


# 行业能力

## 扫码点餐

### 基础功能
| 接口英文名 | 接口中文名 | 接口描述 |
| --- | --- | --- |
| [alipay.trade.create](https://docs.open.alipay.com/api_1/alipay.trade.create) | 统一收单交易创建接口 | 商户通过该接口创建交易订单，获取支付宝订单号。 |
| [alipay.open.app.qrcode.create](https://opendocs.alipay.com/mini/api/openapi-qrcode) | 小程序二维码生成接口 | 生成小程序推广二维码。 |


### 扩展功能
| 接口英文名 | 接口中文名 | 接口描述 |
| --- | --- | --- |
| [alipay.merchant.order.sync](https://opendocs.alipay.com/apis/api_4/alipay.merchant.order.sync) | 订单数据同步接口 | 商户可以调用此接口同步交易对应的订单数据。 |

