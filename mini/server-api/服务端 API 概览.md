# 简介

本文概述了小程序开放能力涉及的服务端 API 及其作用，更多接口使用详情参见 [开放能力](https://opendocs.alipay.com/mini/00am3f)。

**说明：**

- 更多接口文档参见 [API](https://opendocs.alipay.com/apis)。
- 服务端 SDK 使用前，请下载 [开发工具包（SDK）](https://opendocs.alipay.com/open/54/cyz7do#%E6%9C%8D%E5%8A%A1%E7%AB%AF%20SDK)。

# 基础能力

## 小程序二维码

| 接口英文名 | 接口中文名 | 接口描述 |
| --- | --- | --- |
| [alipay.open.app.qrcode.create](https://opendocs.alipay.com/mini/02ovqp) | 小程序生成推广二维码接口 | 生成小程序推广二维码。 |

## 用户授权

| 接口英文名 | 接口中文名 | 接口描述 |
| --- | --- | --- |
| [alipay.system.oauth.token](https://opendocs.alipay.com/mini/02qkj4) | 换取授权访问令牌 | 换取授权访问令牌。 |

## 小程序订单中心

| 接口英文名 | 接口中文名 | 接口描述 |
| --- | --- | --- |
| [alipay.merchant.item.file.upload](https://opendocs.alipay.com/mini/02ctgk) | 商品文件上传 | 商户把商品对应的图片文件、普通文件信息上传到支付宝，后续通过该接口返回的素材 ID 来和支付宝交互。 |
| [alipay.merchant.order.sync](https://opendocs.alipay.com/mini/02qflw) | 订单数据同步 | 商户可以调用此接口同步对应订单数据至小程序订单中心。 |
| [spi.alipay.merchant.order.realtimeinfo.query](https://opendocs.alipay.com/mini/02qh1d) | 商户订单实时信息查询 | 商户同步小程序订单到订单中心，在 C 端场景需要透传订单相关的实时信息时，商户可通过接口返回订单实时信息，如司机距离、配送员位置等信息。 |

## 小程序内容同步

| 接口英文名 | 接口中文名 | 接口描述 |
| --- | --- | --- |
| [alipay.open.mini.content.sync](https://opendocs.alipay.com/mini/02cur3) | 小程序内容接入 | 支持小程序同步小程序服务、商品信息接入、门店绑定内容类型。 |
| [alipay.open.app.appcontent.function.create](https://opendocs.alipay.com/mini/02ctgp) | 小程序服务创建 | 创建小程序服务，获取小程序服务 code。 |
| [alipay.open.app.appcontent.function.query](https://opendocs.alipay.com/mini/02cur4) | 小程序服务查询 | 查询小程序服务的审核状态。 |
| [alipay.open.app.appcontent.function.modify](https://opendocs.alipay.com/mini/02ctgq) | 小程序服务编辑 | 小程序服务被驳回需要重新提审或修改服务基础信息时，可以通过接口来编辑服务并提交审核。 |
| [alipay.open.app.appcontent.function.offline](https://opendocs.alipay.com/mini/02cur5) | 小程序服务失效 | 当小程序服务需要删除时，可以通过接口来删除服务。服务被删除后，该服务无法再在 C 端被曝光。 |
| [alipay.open.mini.item.batchquery](https://opendocs.alipay.com/mini/02cur6) | 小程序商品批量查询 | 小程序商品批量查询。 |
| [alipay.open.mini.item.page.query](https://opendocs.alipay.com/mini/02cur7) | 小程序商品分页查询 | 小程序商品分页查询。 |
| [alipay.open.mini.shop.relation.bind](https://opendocs.alipay.com/mini/02ctgs) | 小程序门店绑定 | 小程序门店绑定。 |
| [alipay.open.mini.shop.relation.query](https://opendocs.alipay.com/mini/02cur8) | 小程序门店关系查询 | 查询小程序门店关系。 |

## 蚂蚁门店管理

| 接口英文名 | 接口中文名 | 接口描述 |
| --- | --- | --- |
| [ant.merchant.expand.shop.query](https://opendocs.alipay.com/mini/02cura) | 店铺查询接口 | 用于查询对应账号下拥有支付宝门店信息。 |
| [ant.merchant.expand.shop.save.passed](https://opendocs.alipay.com/mini/02curb) | 店铺审核通过消息 | 创建蚂蚁门店接口中创建商户审核通过后，支付宝通过本接口推送成功消息至应用网关。 |
| [ant.merchant.expand.shop.create](https://opendocs.alipay.com/mini/02curc) | 蚂蚁店铺创建 | 创建蚂蚁门店（即支付宝门店）。 |
| [ant.merchant.expand.shop.modify](https://opendocs.alipay.com/mini/02curd) | 修改蚂蚁店铺 | 修改蚂蚁门店信息，按信息项修改。若无特殊说明，如果某项存在但是没填写，则不会覆盖掉原来的值。 |
| [ant.merchant.expand.order.query](https://opendocs.alipay.com/mini/02ctgt) | 商户申请单查询 | 开发者可根据申请单 ID，查询自己提交的商户进件、管理等申请单。 |
| [ant.merchant.expand.shop.close](https://opendocs.alipay.com/mini/02cure) | 蚂蚁店铺关闭 | 通过 shop_id 关闭蚂蚁门店。 |
| [ant.merchant.expand.shop.save.rejected](https://opendocs.alipay.com/mini/02ctgu) | 店铺审核拒绝通过消息 | 创建蚂蚁门店接口中创建商户审核失败后，支付宝通过本接口推送审核失败消息至应用网关。 |
| [ant.merchant.expand.indirect.image.upload](https://opendocs.alipay.com/mini/02ctgv) | 图片上传 | 图片资料上传。 |
| [ant.merchant.expand.shop.page.query](https://opendocs.alipay.com/mini/02ctgw) | 店铺分页查询接口 | 用于服务商或商户查询其自己的店铺信息。 |

# 支付能力

## 小程序支付

| 接口英文名 | 接口中文名 | 接口描述 |
| --- | --- | --- |
| [alipay.trade.create](https://opendocs.alipay.com/mini/02j1c4) | 统一收单交易创建接口 | 商户通过该接口进行交易的创建下单。 |
| [alipay.open.agent.facetoface.sign](https://opendocs.alipay.com/mini/02j2c1) | 代签约当面付接口（也适用于服务商代替商户签约小程序支付） | 三方应用代理签约当面付产品，需要配合开启事务接口使用。 |

# 资金能力

## 周期扣款

### 签约接口

| 接口英文名 | 接口中文名 | 接口描述 |
| --- | --- | --- |
| [alipay.user.agreement.page.sign](https://opendocs.alipay.com/mini/02fkb3?scene=35) | 支付宝个人协议页面签约接口 | 开发者可通过该接口传入周期扣款协议相关限制内容，生成签约参数用于小程序唤起签约页面。<br />目前支持支付宝钱包 H5 页面签约、扫码签约等方式。 |
| [alipay.user.agreement.query](https://opendocs.alipay.com/mini/02fkb4?scene=8837b4183390497f84bb53783b488ecc) | 支付宝个人代扣协议查询接口 | 支付宝个人代扣协议查询接口，通过该接口可查询用户协议信息。 |
| [alipay.user.agreement.unsign](https://opendocs.alipay.com/mini/02fit0?scene=90766afb41f74df6ae1676e89625ebac) | 支付宝个人代扣协议解约接口 | 支付宝个人代扣协议解约接口，通过该接口可解除用户在约协议。 |
| [alipay.user.agreement.executionplan.modify](https://opendocs.alipay.com/mini/02fit1) | 周期性扣款协议执行计划修改接口 | 通过该接口，商户可以实现延期扣款。 |
| [alipay.user.agreement.transfer](https://opendocs.alipay.com/mini/02fit2) | 协议由普通通用代扣协议产品转移到周期扣协议产品 | 商户通过接口将普通通用的代扣协议转移成周期扣款协议。 |

### 支付接口

| 接口英文名 | 接口中文名 | 接口描述 |
| --- | --- | --- |
| [alipay.trade.pay](https://opendocs.alipay.com/mini/02d2xs?scene=33) | 统一收单交易支付接口 | 用户在完成协议签约后，商户可通过本接口完成协议规定的后续代扣。 |
| [alipay.trade.app.pay](https://opendocs.alipay.com/mini/02d1g0) | APP 支付 2.0 接口 | 外部商户 APP 唤起快捷 SDK 创建订单并支付。 |
| [alipay.trade.refund](https://opendocs.alipay.com/mini/02d2xt) | 统一收单交易退款接口 | 当交易发生之后一段时间内，卖家可以通过退款接口将支付款退还给买家，支付宝按照退款规则将支付款按原路退到买家帐号上。 |
| [alipay.trade.query](https://opendocs.alipay.com/mini/02d2xu) | 统一收单线下交易查询 | 该接口提供所有支付宝支付订单的查询，商户可以通过该接口主动查询支付订单状态，完成下一步的业务逻辑。 |
| [alipay.trade.cancel](https://opendocs.alipay.com/mini/02d2xv) | 统一收单交易撤销接口 | 支付交易返回失败或支付系统超时，调用该接口撤销交易。 |
| [alipay.trade.close](https://opendocs.alipay.com/mini/02d2xw) | 统一收单交易关闭接口 | 用于交易创建后，用户在一定时间内未进行支付，可调用该接口直接将未付款的交易进行关闭。 |

## 商家分账

### 分账关系维护

| 接口英文名 | 接口中文名 | 接口描述 |
| --- | --- | --- |
| [alipay.trade.royalty.relation.bind](https://opendocs.alipay.com/mini/02d1g4) | 分账关系绑定 | 开发者可通过该接口批量维护商家与分账方关系，批量进行分账关系绑定。 |
| [alipay.trade.royalty.relation.unbind](https://opendocs.alipay.com/mini/02d1g5) | 分账关系解绑 | 开发者可通过该接口批量维护商家与分账方关系，批量进行分账关系解绑。 |
| [alipay.trade.royalty.relation.batchquery](https://opendocs.alipay.com/mini/02d1g6) | 分账关系查询 | 开发者可通过该接口批量维护商家与分账方关系，分页查询分账关系。 |

### 分账请求接口

| 接口英文名 | 接口中文名 | 接口描述 |
| --- | --- | --- |
| [alipay.trade.order.settle](https://opendocs.alipay.com/mini/02d1g7) | 统一收单交易结算接口 | 用于在线下场景交易支付后，进行卖家与第三方（如供应商或平台商）基于交易金额的分佣结算。 |

### 分账查询接口

| 接口英文名 | 接口中文名 | 接口描述 |
| --- | --- | --- |
| [alipay.trade.query](https://opendocs.alipay.com/mini/02d2y0) | 统一收单线下交易查询接口 | 用于卖家与第三方（如供应商或平台商）基于交易金额的已分佣明细查询。通过传递 "query_options":["TRADE_SETTE_INFO"] 参数查询分账明细。 |

### 退款退分账接口

| 接口英文名 | 接口中文名 | 接口描述 |
| --- | --- | --- |
| [alipay.trade.refund](https://opendocs.alipay.com/mini/02d1g9) | 统一收单交易退款接口 | 用于卖家与第三方（如供应商或平台商）基于交易金额的退分佣信息。<br />通过 refund_royalty_parameters 传递退分佣信息。 |

## 转账到支付宝账户

| 接口英文名 | 接口中文名 | 接口描述 |
| --- | --- | --- |
| [alipay.fund.trans.uni.transfer](https://opendocs.alipay.com/mini/02d2y1?scene=ca56bca529e64125a2786703c6192d41) | 用于向指定支付宝账户转账 | 单笔转账接口是基于支付宝的资金处理能力，提供通过 API 接口完成企业自身支付宝账户到支付宝账户、企业自身支付宝账户到银行卡的转账功能。 |
| [alipay.fund.trans.common.query](https://opendocs.alipay.com/mini/02d2y2?scene=f9fece54d41f49cbbd00dc73655a01a4) | 用于查询转账结果 | 商户可通过该接口查询转账业务单据的状态。 |
| [alipay.fund.account.query](https://opendocs.alipay.com/mini/02d2y3?scene=c76aa8f1c54e4b8b8ffecfafc4d3c31c) | 用于查询支付宝账户余额 | 可查询请求方的支付宝账户余额信息。 |
| [alipay.fund.trans.order.changed](https://opendocs.alipay.com/mini/02d2y4) | 用于转账单据状态变更后触发的通知 | 单笔转账到支付宝账户、单笔转账到银行卡、C2C 现金红包、B2C 现金红包单据状态变更后触发的通知。 |

## 支付宝预授权

| 接口英文名 | 接口中文名 | 接口描述 |
| --- | --- | --- |
| [alipay.fund.auth.order.app.freeze](https://opendocs.alipay.com/mini/02f0g0) | 线上资金授权冻结接口 | 创建支付宝授权订单并完成资金冻结。适用于线上场景完成资金授权，例如从商户 APP 端拉起支付宝收银台完成冻结。 |
| [alipay.fund.auth.order.unfreeze](https://opendocs.alipay.com/mini/02f1pm) | 资金授权解冻接口 | 商家可将需要解冻的授权资金通过该接口进行解冻。支付宝在收到解冻请求并验证成功后，依循解冻规则将冻结资金按原路解冻。 |
| [alipay.fund.auth.operation.cancel](https://opendocs.alipay.com/mini/02f1pp) | 资金授权撤销接口 | 只有商户由于业务系统处理超时需要终止后续业务处理或者授权结果未知时可调用撤销，其他正常授权冻结的操作如需实现相同功能请调用 资金授权解冻接口。<br />提交资金授权后调用 资金授权操作查询，没有明确的授权结果再调用 资金授权撤销。 |
| [alipay.fund.auth.operation.detail.query](https://opendocs.alipay.com/mini/02f0g1) | 资金授权操作查询接口 | 通过该接口可以查询单笔明细的详细信息。 |
| [alipay.trade.pay](https://opendocs.alipay.com/mini/02cth5?scene=34) | 统一收单交易支付接口 | 用户在完成协议签约后，商户将用户签约协议号通过本接口送至支付宝完成代扣支付。 |
| [alipay.trade.query](hhttps://opendocs.alipay.com/mini/02cth6) | 统一收单线下交易查询 | 该接口提供所有支付宝支付订单的查询，商户可以通过该接口主动查询订单状态，完成下一步的业务逻辑。 |
| [alipay.trade.refund](https://opendocs.alipay.com/mini/02cqrq) | 统一收单交易退款接口 | 当交易发生之后一段时间内，卖家可以通过退款接口将支付款退还给买家，支付宝按照退款规则将支付款按原路退到买家帐号上。 |
| [alipay.trade.orderinfo.sync](https://opendocs.alipay.com/mini/02cs7m) | 支付宝订单信息同步接口 | 该接口用于商户向支付宝同步该笔订单相关业务信息。 |
| [alipay.data.dataservice.bill.downloadurl.query](https://opendocs.alipay.com/mini/02cs7l) | 查询对账单下载地址 | 为方便商户快速查账，支持商户通过本接口获取商户离线账单下载地址。 |

# 会员能力

## 商户会员卡

### 基础接口

| 接口英文名 | 接口中文名 | 接口描述 |
| --- | --- | --- |
| [alipay.offline.material.image.upload](https://docs.open.alipay.com/api_3/alipay.offline.material.image.upload) | 图片资料上传 | 开发者需先将要使用的图片上传至支付宝服务器，获取对应的图片 ID 用于后续配置会员卡模板等接口。 |

### 会员卡模板管理

| 接口英文名 | 接口中文名 | 接口描述 |
| --- | --- | --- |
| [alipay.marketing.card.template.create](https://opendocs.alipay.com/mini/02drvb) | 会员卡模板创建 | 会员卡模板创建。 |
| [alipay.marketing.card.template.modify](https://opendocs.alipay.com/mini/02drvc) | 会员卡模板修改 | 开发者可调用该接口修改制定会员卡模板。<br />注意：<br />1.修改会员卡模板后，该模板下所有会员卡都会更新（ 包括已发放会员卡）。<br />2.修改会员卡模板，field_rule_list（字段规则列表）配置项不支持修改，设置后无效。<br />3.会员卡设置 shop_ids 后，shop_ids 只支持新增或修改门店，但是不支持删除 shop_ids 参数。<br />4.其他修改项因为线上缓存的缘故，模板更新可能存在 1-5 分钟延时。 |
| [alipay.marketing.card.template.query](https://opendocs.alipay.com/mini/02dqk9) | 会员卡模板查询接口 | 会员卡模板查询接口。 |

### 开卡组件

| 接口英文名 | 接口中文名 | 接口描述 |
| --- | --- | --- |
| [alipay.marketing.card.formtemplate.set](https://opendocs.alipay.com/mini/02drvd) | 会员卡开卡表单模板配置 | 开发者可通过本接口配置用户开卡时需提交信息。 |
| [alipay.marketing.card.activateurl.apply](https://opendocs.alipay.com/mini/02drve) | 获取会员卡领卡投放链接 | 会员卡开卡业务，开发者通过该接口获取用户开卡链接，用于会员卡投放。<br />小程序场景中无需传入 callback 地址。 |
| [alipay.marketing.card.activateform.query](https://opendocs.alipay.com/mini/02dt9c) | 查询用户提交的会员卡表单信息 | 会员卡开卡场景下，用户确认领卡后，跳转到商户开卡处理页面，商户通过该接口查询用户表单信息。 |

### 会员卡管理

| 接口英文名 | 接口中文名 | 接口描述 |
| --- | --- | --- |
| [alipay.marketing.card.open](https://opendocs.alipay.com/mini/02drvf) | 会员卡开卡 | 开发者可调用本接口给用户开卡，成功后会员卡将自动添加至用户卡包。 |
| [alipay.marketing.card.update](https://opendocs.alipay.com/mini/02drvg) | 会员卡更新 | 开发者可调用本接口更新用户开取的某张会员卡信息，如积分等。<br />注意：<br />1.更新会员卡后，只有该张会员卡会进行更新，其他会员卡不会更新。<br />2.open_date（开卡时间）和 valid_date（结束时间）不支持修改，设置后无效。<br />3.不支持设置 notify_messages（卡信息变更通知消息），设置后无效，不会发送通知。<br />4.其他修改项因为线上缓存的缘故，模板更新可能存在 1-5 分钟延时。 |
| [alipay.marketing.card.delete](https://opendocs.alipay.com/mini/02drvh) | 会员卡删卡 | 开发者可通过本接口删除用户开取的会员卡。 |
| [alipay.marketing.card.query](https://opendocs.alipay.com/mini/02drvi) | 会员卡查询 | 根据卡号或者持卡人信息查询用户在开卡页面提交的信息。 |

## 支付宝身份验证

| 接口英文名 | 接口中文名 | 接口描述 |
| --- | --- | --- |
| [alipay.user.certify.open.query](https://opendocs.alipay.com/mini/02osih) | 身份认证记录查询 | 商户在开放认证完成后，调用本接口查询认证状态和相关数据。 |
| [alipay.user.certify.open.initialize](https://opendocs.alipay.com/mini/02oqix) | 身份认证初始化服务 | 开发者可调用本接口，传入用户实名信息初始化支付宝开放认证服务，创建开放认证流程并获取 certify_id。 |
| [alipay.user.certify.open.certify](https://opendocs.alipay.com/mini/02osii) | 身份认证开始认证 | 在完成开放认证初始化后，开发者可调用本接口开始认证流程，获取身份验证链接用于小程序跳转至身份验证页。 |

# 营销能力

## 支付宝卡包

| 接口英文名 | 接口中文名 | 接口描述 |
| --- | --- | --- |
| [alipay.pass.template.add](https://opendocs.alipay.com/mini/02dodm) | 卡券模板创建接口 | 创建卡券的模板，卡券的样式、内容信息通过该接口提交到支付宝，支付宝会生成模板 ID 反馈给开发者，用于后续的更新和发放。 |
| [alipay.pass.template.update](https://opendocs.alipay.com/mini/02du98) | 卡券模板更新接口 | <br />对于已经创建的模板，如果需要修改模板内容，可通过该接口修改，适用于修改模板内容。<br />对于已经发布的模板，如果需要修改内容并同步到用户端，则应使用 卡券实例更新接口。 |
| [alipay.pass.instance.add](https://opendocs.alipay.com/mini/02dodn) | 卡券实例发放接口 | 卡券模板生成后，如需将卡券发布给对应的用户，则调用此接口。 |
| [alipay.pass.instance.update](https://opendocs.alipay.com/mini/02du99) | 卡券实例更新接口 | 对于已经发布的卡券，如需更新内容，可通过此接口更新，主要用于更新卡券的使用状态。 |
| [alipay.user.pass.instancebatch.add](https://opendocs.alipay.com/mini/02du9a) | 卡券实例批量发放接口 | 商家向用户一次性发放多张卡券时使用，常被称作优惠大礼包。支付宝将保证批次的事务型，即全部发放成功或全部发放失败。 |

## 现金红包

| 接口英文名 | 接口中文名 | 接口描述 |
| --- | --- | --- |
| [alipay.fund.trans.uni.transfer](https://opendocs.alipay.com/mini/02pj6g) | 统一转账接口 | 单笔转账接口是基于支付宝的资金处理能力，提供通过 API 接口完成企业自身支付宝账户到支付宝账户、企业自身支付宝账户到银行卡的转账功能。 |
| [alipay.fund.trans.common.query](https://opendocs.alipay.com/mini/02pj6h) | 单据查询接口 | 商户可通过该接口查询转账业务单据的状态。 |
| [alipay.fund.trans.order.changed](https://opendocs.alipay.com/mini/02pk59) | 单据状态变更后触发的通知接口 | 单笔转账到支付宝账户、单笔转账到银行卡、C2C 现金红包、B2C 现金红包单据状态变更后触发的通知。 |

## 无资金商户优惠券

| 接口英文名 | 接口中文名 | 接口描述 |
| --- | --- | --- |
| [alipay.marketing.cashlessvoucher.template.create](https://opendocs.alipay.com/mini/02drvq) | 无资金券模板创建接口 | 创建无资金全场优惠券模板。<br />- 全场优惠券暂时只支持"无资金代金券"(CASHLESS_FIX_VOUCHER)。 |
| [alipay.marketing.cashlessvoucher.template.modify](https://opendocs.alipay.com/mini/02dt9j) | 无资金券模板修改接口 | 修改无资金券模板。 |
| [alipay.marketing.voucher.send](https://opendocs.alipay.com/mini/02drvr) | 发券接口 | 开发者可调用本接口通过用户 user_id 向用户发券。 |
| [alipay.marketing.voucher.templatedetail.query](https://opendocs.alipay.com/mini/02dt9k) | 查询模板详情 | 查询模板的详细信息，包含准实时的汇总信息。 |
| [alipay.marketing.voucher.templatelist.query](https://opendocs.alipay.com/mini/02drvs) | 查询券模板列表 | 分页查询当前 PID 下的所有模板。 |
| [alipay.marketing.voucher.query](https://opendocs.alipay.com/mini/02dt9l) | 券查询 | 商户券信息查询。 |
| [alipay.marketing.userule.pid.query](https://opendocs.alipay.com/mini/02drvt) | 商户使用场景规则 PID 查询 | 查询商户可用于使用场景规则的 PID。 |
| [ant.merchant.expand.merchant.storelist.query](https://opendocs.alipay.com/mini/02drvu) | 商户外部门店查询接口 | 查询商户外部门店。 |
| [alipay.marketing.material.image.upload](https://opendocs.alipay.com/mini/02dt9m) | 营销图片上传接口 | 开发者可调用本接口上传单品优惠券模板中使用的商品图片，获取图片 id。 |
| [alipay.marketing.cashlessitemvoucher.template.create](https://opendocs.alipay.com/mini/02dt9n) | 无资金单品券创建接口 | 开发者可调用本接口创建无资金单品优惠券模板。 |

## 模板消息

| 接口英文名 | 接口中文名 | 接口描述 |
| --- | --- | --- |
| [alipay.open.app.mini.templatemessage.send](https://opendocs.alipay.com/mini/02cth2) | 小程序发送模板消息 | 小程序通过 OpenAPI 给用户触达消息，主要为支付后的触达（通过支付宝订单号 trade_no）、用户提交表单后的触达（通过 formId）。 |

# 安全能力

## e 签宝电子合同

### 合同模板相关接口

| 接口英文名 | 接口中文名 | 接口描述 |
| --- | --- | --- |
| [alipay.eco.doc.template.create](https://opendocs.alipay.com/mini/02plhl) | 创建合同模板 | 调用接口创建合同模板，通过获取到的 uploadUrl 进行文件流上传 Word/PDF 文件，文件上传后模板才可使用。 |
| [alipay.eco.doctemplate.settingurl.query](https://opendocs.alipay.com/mini/02pmir) | 获取合同模板设置地址 | 调用接口获取已经创建并上传文件的合同模板设置页面地址。 |

### 合同签署相关接口

| 接口英文名 | 接口中文名 | 接口描述 |
| --- | --- | --- |
| [alipay.eco.contract.signflows.create](https://opendocs.alipay.com/mini/02pmis) | 创建签署流程 | 基于合同模板创建合同签署流程。调用此接口前，需完成模版创建及组件设置。 |
| [alipay.eco.sign.flow.query](hhttps://opendocs.alipay.com/mini/02plhn) | 签署流程查询 | 可通过此接口查询流程、签署人的签署状态。 |
| [alipay.eco.signflows.url.query](https://opendocs.alipay.com/mini/02plho) | 获取流程签署地址 | 创建签署流程后，可通过此接口获取指定签署人的签署链接。 |
| [alipay.eco.signflows.detail.query](https://opendocs.alipay.com/mini/02pmit) | 流程文档下载 | 可通过此接口获取签署流程合同与附件的下载地址。 |
| [alipay.eco.file.path.query](https://opendocs.alipay.com/mini/02pmiv) | 获取文件直传地址 | 通过获取到的 uploadUrl 进行文件流上传合同的附件，如订单截图等，可作为电子合同的辅助证明材料。上传文件具体注意事项参见 [文件流上传方法](https://opendocs.alipay.com/mini/00kr2w)。 |
| [alipay.eco.sign.flow.cancel](https://opendocs.alipay.com/mini/02pmiw) | 签署流程撤销 | 可通过此接口撤销合同签署流程。场景举例：用户取消订单后，需通过流程 ID（flow_id）撤销对应的电子合同签署流程。 |

## 文本风险识别

| 接口英文名 | 接口中文名 | 接口描述 |
| --- | --- | --- |
| [alipay.security.risk.content.detect](https://docs.open.alipay.com/api_49/alipay.security.risk.content.detect) | 文本风险识别（服务端） | 蚁盾为小程序提供的用于内容风险检测的服务，适用范围仅限于正在使用小程序的商户。 |

# 行业能力

## 扫码点餐

### 基础功能

| 接口英文名 | 接口中文名 | 接口描述 |
| --- | --- | --- |
| [alipay.trade.create](https://opendocs.alipay.com/mini/02du9h) | 统一收单交易创建接口 | 商户通过该接口创建交易订单，获取支付宝订单号。 |
| [alipay.open.app.qrcode.create](https://opendocs.alipay.com/mini/02dwlu) | 小程序二维码生成接口 | 生成小程序推广二维码。 |

### 扩展功能

| 接口英文名 | 接口中文名 | 接口描述 |
| --- | --- | --- |
| [alipay.merchant.order.sync](https://opendocs.alipay.com/mini/02dvdb) | 订单数据同步接口 | 商户可以调用此接口同步交易对应的订单数据。 |
