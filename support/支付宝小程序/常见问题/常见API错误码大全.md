| **API** | **error** | **errorMessage** | **解决方案** |
| --- | --- | --- | --- |
| [my.request](https://opendocs.alipay.com/mini/api/owycmh) | 1 | 请求没有结束，就跳转到了另一个页面。 | <br />1. 建议请求完成后再进行页面跳转，可以在页面加上对应的加载提示（如：[my.showLoading](https://opendocs.alipay.com/mini/api/bm69kb)）。<br />2. 如需强行做页面跳转操作，建议加上[RequestTask.abort()](https://opendocs.alipay.com/mini/api/owycmh#%E8%BF%94%E5%9B%9E%E5%80%BC%20RequestTask) 中断请求任务。<br /> |
|  | 2 | 参数错误。 | <br />1. 可能是链接过长导致，建议参数放在 data 中处理。<br />2. 建议检查请求时传递的数据是否正常，格式是否正确，可以在请求前打印下入参数据日志。<br /> |
|  | 4/11 | 无权调用该接口。 | <br />1. 没有配置请求白名单导致，检查请求域名是否添加了域名白名单，请预先在 [开放平台控制台](https://open.alipay.com/mini/dev/list) > 小程序详情页 >**  开发设置** > **服务器域名白名单 **中配置域名白名单。小程序在以下 API 调用时只能与白名单中的域名进行通讯：HTTP 请求（my.request）、上传文件（my.uploadFile），添加后请重新生成预览/体验版进行测试。<br />2. 若是账号问题，不能登录管理控制台配置，开发版测试可以先在开发工具IDE左上角点击 **详情** > **域名信息** 下勾选 **忽略 request 域名合法性检查**（仅在本地模拟、预览和远程调试时生效）或 忽略 Webview 域名合法性检查（仅在本地模拟、预览和远程调试时生效），再预览调试请求。<br />
**注意：**<br />- 新版本上架，一定要添加 服务器域名白名单，否则会出现异常。<br />- request 请求的地址域名可能写错，导致与配置的请求白名单域名不一致，请仔细检查。<br /> |
|  | 12 | 网络出错。 | 建议检查网络环境是否正常，服务器是否稳定。 |
|  | 13 | 超时。 | 建议检查网络环境是否正常，服务器是否正常响应，若请求需要时间长，可适当设置超时时间 timeout。 |
|  | 14 | JSON parse data error | <br />1. 解码失败。<br />   - dataType 为 JSON：小程序框架对返回结果做 JSON.prase 操作时解析失败。

   - dataType 为 text：返回的内容格式不符。

   - dataType 为 base64：转换失败

2. 建议检查前服务端请求和响应数据格式是否一致；如：返回数据格式 text 与入参 dataType 值 JSON 不一致而导致接口报错，请修改服务端返回数据格式为 JSON。<br />**注意：**如果服务端是 PHP 或 .Net，可检查响应的内容中是否携带了 bom，一般是相关代码文件或者配置文件携带 bom，可以搜索引擎搜索 清除 utf-8 bom 头，可在在线接口测试工具上查看是否带 bom。<br />3. 若服务端要返回非 JSON 字符串则需要把 my.request 的 dataType 参数设置成 text。<br />4. 保证 SSL 证书链完整并且证书不过期，可以使用证书工具或者咨询服务器提供商如阿里云进行验证。<br /> |
|  | 15 | 传参失败。 | 小程序页面传参如果做 urlencode 需要把整体参数进行编码。 |
|  | 19 | HTTP 错误。 | <br />1. 请确认请求 URL 地址在外网是否能正常请求，HTTPS 协议，小程序真机上都是生产环境的正式请求，不能使用局域网本地请求。<br />2. 一般如 HTTP 404、500、504 等异常错误，建议打开 IDE 调试器 > Network 可以查看具体的错误信息，然后根据对应 HTTP 错误码对症处理。<br />3. SSL 证书不正确导致的，建议更换网站 SSL 证书，推荐使用 [阿里云SSL 证书](https://promotion.aliyun.com/ntms/act/sslbuy.html?utm_content=se_1005900042) 或 [Serverless云服务](https://help.aliyun.com/document_detail/121906.html)。<br /> |
|  | 20 | 请求已被停止/服务端限流 | 请确认请求服务器是否能正常请求和响应。 |
|  |  | 请求 URL 不支持 HTTP，请使用 HTTPS | 小程序已经不支持 HTTP 请求，请使用 HTTPS。 |
|  | 23 | 代理请求失败。 | 建议检查代理配置是否正确。 |
| [my.uploadFile](https://opendocs.alipay.com/mini/api/kmq4hc) | 4 | 无权限调（N22104）。 | <br />1. 确认小程序应用是否已授权给三方应用，三方应用是否绑定了 JSAPI 基础包，可尝试添加 JSAPI 基础包后，重新授权、重新推送预览调试或者直接解除三方应用授权，重新推送预览调试。<br />**说明：**小程序应用授权给三方应用后，小程序在真机上的运行使用的是三方应用的产品，不再是使用小程序自身的产品。<br />2. 若是小程序应用 JSAPI 基础包 没有或者不全，建议 [删除小程序应用](https://opendocs.alipay.com/support/01rb3s)，重新创建一个新小程序应用来调试。<br /> |
|  |  | 无权限调（N22106）。 | <br />1. 配置请求白名单，请预先在 [开放平台控制台](https://open.alipay.com/mini/dev/list) > 小程序详情页 >  **开发设置** > **服务器域名白名单** 中配置域名白名单。小程序在以下 API 调用时只能与白名单中的域名进行通讯：HTTP 请求（my.request）、上传文件（my.uploadFile），添加后请重新生成预览/体验版进行测试。<br />2. 若是账号问题，不能登录管理配置，可以先在开发工具IDE左上角点击 详情 > 域名信息 下勾选 忽略 request 域名合法性检查（仅在本地模拟、预览和远程调试时生效）或 忽略 Webview 域名合法性检查（仅在本地模拟、预览和远程调试时生效），再预览调试请求。<br />3. 建议做下兼容，不要使用 my.saveFile 保存文件后返回的 apFilePath 作为上传 filePath 的入参。<br /> |
|  |  | 无权限调用此接口 |  |
|  | 9 | uploadFile:fail abort | 上传文件中止文件，在上传文件未完成时调用了 UploadTask.abort()。 |
|  | 11 | not have permission to upload | 出于安全策略，不能使用 my.saveFile 保存文件后返回的 apFilePath 作为上传 filePath 的入参。 |
|  |  | 文件不存在。 | 检查本地文件是否存在。 |
|  | 12 | java.io.FileNotFoundException:File is not a normal file. | 文件未找到/文件不是一个正常的文件，确认 filePath 入参的正确性，必须是本地定位符，可通过 [my.chooseImage](https://opendocs.alipay.com/mini/api/media/image/my.chooseimage) 在相册选择图片后返回的地址。 |
|  |  | 上传文件失败。 | <br />- 文件过大。<br />- 上传时间超过 30s。<br /> |
|  | 13 | 没有权限 | 检查权限设置。 |
|  | 20 | 请求 URL 不支持 HTTP，请使用 HTTPS | 小程序已经不支持 HTTP 请求，请使用 HTTPS。 |
| [my.tradePay](https://opendocs.alipay.com/mini/api/openapi-pay) | 4 | 无权限调（N22104）。 | 个人小程序应用没有开放小程序支付能力，如需调用请 IDE 关联企业小程序后重新真机调试/预览。 |
|  | 9000 | 订单处理成功。 | 不建议根据 my.tradePay 接口同步返回判断是否支付成功，9000不能判定就是支付成功，请以异步通知（notify_url）返回的 trade_status(交易状态)为 TRADE_SUCCESS + [alipay.trade.query](https://opendocs.alipay.com/open/02e7gm) 接口查询订单是否支付成功实际返回的支付状态为准。 |
|  | 8000 | 正在处理中。支付结果未知（有可能已经支付成功），请查询商家订单列表中订单的支付状态。 | 请调用 [alipay.trade.query](https://opendocs.alipay.com/open/02e7gm) 查询商家订单列表中订单的支付状态，以查询接口实际返回的支付状态为准。 |
|  | 4000 | 订单处理失败。 | tradeNO 调用 [小程序支付](https://opendocs.alipay.com/mini/introduce/pay) 时必填，orderStr 调用 [资金授权](https://opendocs.alipay.com/mini/introduce/pre-authorization) 时必填，二选一，根据具体接入的产品选择参数。<br />小程序支付时：<br />- 检查入参字段 tradeNO 是否编写正确，NO 都是大写。<br />- tradeNO 的入参数据是 [alipay.trade.create](https://opendocs.alipay.com/open/02ekfj) 返回的 trade_no，不是 out_trade_no。<br />
资金授权时：<br />- orderStr 必填。<br />- [alipay.fund.auth.order.app.freeze](https://opendocs.alipay.com/open/02f912) 接口的参数有误，导致通过 response.sdkExcute(request) 方法获取到的orderStr 参数有问题，检查入参字段和数据是否符合接口要求，建议只传必传参数测试，避免其它参数干扰。<br /> |
|  | 6001 | 用户中途取消。 | <br />- 请用户重新签约/支付。<br />- 检查 tradeNO 的入参是否正常入参，参数数据为 [alipay.trade.create](https://opendocs.alipay.com/open/02ekfj) 接口返回的 trade_no。<br />- [alipay.trade.create](https://opendocs.alipay.com/open/02ekfj) 接口在小程序场景中 buyer_id 参数必填，且入参的 buyer_id（用户 user_id，2088 开头）的必须和前端唤起支付的支付宝账号一致。<br /> |
|  | 6002 | 网络连接出错。 | 检查网络连接后重试。 |
|  | 6004 | 处理结果未知（有可能已经成功），请查询商家订单列表中订单状态。 | 请调用 [alipay.trade.query](https://opendocs.alipay.com/open/02e7gm) 接口查询商家订单列表中订单的支付状态，以查询接口实际返回的支付状态为准。 |
|  | 99 | iOS 客户端用户点击忘记密码导致快捷界面退出。 | 用户解决密码问题后，重新发起支付。 |
| [my.ap.navigateToAlipayPage](https://opendocs.alipay.com/mini/api/navigatetoalipaypage) | 2 | 参数错误，打开失败。 | <br />1. 建议检查 H5 页面链接地址 scheme 或 URL 是否有误，可以修改错误 H5 页面链接。<br />2. appCode入参是否有空格、填写正确，参数值必须为文档提个的跳转场景值。<br />3. path 和 appCode 二选一，必填。<br />4. 可跳转域名以 [https://render.alipay.com/p](https://render.alipay.com/p) 开头的支付宝业务、运营页面（生活号文章链接等）。部分支付宝运营、业务页面目前暂不开放跳转。<br /> |
|  | 4 | 无权限调（N22104）。 | 个人小程序应用没有开放 [my.ap.navigateToAlipayPage](https://opendocs.alipay.com/mini/api/navigatetoalipaypage) 能力，如许调用请 IDE 关联企业小程序后重新真机调试/预览。 |
| [my.getAuthCode](https://opendocs.alipay.com/mini/api/openapi-authorize) | 4 | 无权限调（N22104）。 | <br />1. 确认小程序应用是否授权给了三方应用，三方应用是否添加了 JSAPI 基础包，可尝试绑定 JSAPI 基础包，重新授权、重新推送预览调试或者直接解除三方应用授权，重新推送预览调试。<br />**说明：**小程序应用授权给三方应用后，小程序在真机上的运行使用的是三方应用的产品，不再是使用小程序自身的产品。<br />2. 若是小程序应用 JSAPI 基础包 没有或者不全，建议 [删除小程序应用](https://opendocs.alipay.com/support/01rb3s)，重新创建一个新小程序应用来调试。<br /> |
|  | 10 | Empty Data | <br />1. 为了创造更良好的支付宝小程序用户体验，在小程序的首屏引导用户授权是不被允许的。需要在用户充分了解小程序的业务内容后再引导用户授权，建议将小程序授权环节放在业务流程中。<br />2. 检查 scopes 入参是否正确，详情可查看 [入参参数列表](https://opendocs.alipay.com/mini/api/openapi-authorize)（参数错误会先弹出 **服务正忙，请稍后再试**）。<br />3. 建议在需要获取用户信息前，增加获取权限的用途和引导提示，引导用户接受小程序授权，增加用户体验。<br />4. 在 fail 做引导处理，重新调用 my.getAuthCode 授权。<br /> |
|  | 11 | 用户取消授权 | <br />1. 为了创造更良好的支付宝小程序用户体验，在小程序的首屏引导用户授权是不被允许的。需要在用户充分了解小程序的业务内容后再引导用户授权，建议将小程序授权环节放在业务流程中。<br />2. 建议在需要获取用户信息前，增加获取权限的用途和引导提示，引导用户接受小程序授权，增加用户体验。<br />3. 在 fail 做引导处理，重新调用 my.getAuthCode 授权。<br /> |
| [my.getPhoneNumber](https://opendocs.alipay.com/mini/api/getphonenumber) | 1 | 该接口暂不支持 | 由于模拟器不支持模拟 my.getPhoneNumber，IDE开发工具编辑完成相关 API 代码逻辑后，使用真机调试/预览进行调试 API 功能。 |
|  | 40001 | 应用未设置默认签名类型 | <br />1. 配置接口加签方式/接口内容加密方式。<br />   1. 在 [开放平台控制台](https://openhome.alipay.com/mini/dev/list) > **开发设置** 中检查接口加签方式、接口内容加密方式是否已经设置，若没有设置可查看相关设置文档进行设置。<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/179989/1667443187097-954b2c61-0e8e-47e1-bbce-fbb740a68c3b.png#align=left&display=inline&height=259&margin=%5Bobject%20Object%5D&name=image.png&originHeight=518&originWidth=1370&size=76246&status=done&style=none&width=685)<br />   2. 在 **开放平台密钥** 页面点击选择需要配置接口加签方式/接口内容加密方式的应用配置。<br />两个入口选择其一即可完成配置，详细说明请 [设置接口加签方式](https://opendocs.alipay.com/common/02mriz)、[设置接口内容加密方式](https://opendocs.alipay.com/common/02mse3)。<br />2. 检查设置完成后，点击 小程序右上角三个点 > 关于 > 右上角（设置）> 用户信息，解除授权后重新授权获取。<br /> |
|  |  | 缺少加密配置 |  |
|  | 40002 | 加密异常 | <br />- 重新 [设置接口内容加密方式](https://opendocs.alipay.com/common/02mse3)（设置方式同40001）。<br />- 检查设置完成后，点击 小程序右上角三个点 > 关于 > 右上角（设置）> 用户信息，解除授权后重新授权获取。<br /> |
|  | 40003 | 无效授权关系 | 不能直接调用 my.getPhoneNumber 接口，用户主动触发才能发起获取手机号请求，应该先通过 [button 组件](https://opendocs.alipay.com/mini/component/button) 的“点击”动作来进行授权，然后在授权成功回调中调用该接口。 |
|  | 40006 | ISV权限不足 | <br />1. 登录 [开放平台控制台](https://openhome.alipay.com/mini/dev/list) 进入对应小程序详情页的产品绑定中，绑定获取会员手机号。<br />2. 点击用户信息申请，在申请权限中申请用户手机号（需要主账号登录申请），填写申请原因、使用场景等信息，提交申请，等待审核。<br />
**注意：**请确认服务端代码中传入的 APPID 与 PID 需要绑定产品且申请用户信息的小程序与账号信息。 |
| [my.getOpenUserInfo](https://opendocs.alipay.com/mini/api/ch8chh) | 40003 | 无效授权关系 | 不能直接调用 my.getOpenUserInfo 接口，用户主动触发才能发起获取会员基础信息请求，应该先通过 [button 组件](https://opendocs.alipay.com/mini/component/button) 的“点击”动作来进行授权，然后在授权成功回调中调用该接口。 |
|  | 40006 | ISV权限不足 | 登录 [开放平台控制台](https://openhome.alipay.com/mini/dev/list) 进入对应小程序详情页的产品绑定中，绑定获取会员基础信息。 |
| [my.getRunData](https://opendocs.alipay.com/mini/api/gxuu7v) | 1003 | 未授权支付宝应用计步权限 | 引导用户授权获取运动步数功能，建议在获取前增加获取权限的用途和引导提示，引导用户接受小程序授权，增加用户体验。 |
|  | 1005 | 用户未开通支付宝运动功能 | <br />1. my.getRunData 获取运动步数在 IDE 模拟器暂不支持，请在真机调试。<br />2. 在调用 my.getRunData 时，用户未开启 运动步数功能，会自动引导用户跳转 **运动 **官方小程序，用户可点击** 立即开启 **打开功能。<br />3. 支付宝首页搜一搜 运动 官方小程序，进入后开按照提示 去开启 运动步数功能。<br /> |
|  | 40001 | 应用未设置默认签名类型 | <br />1. 配置接口加签方式/接口内容加密方式。<br />在 [开放平台控制台](https://openhome.alipay.com/mini/dev/list) > 小程序详情页 > **开发设置** 中检查接口加签方式、接口内容加密方式是否已经设置，若没有设置可查看相关设置文档进行设置。<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/179989/1667443248037-f0a98db3-2a96-4223-ba99-c6d5a7438123.png#align=left&display=inline&height=259&margin=%5Bobject%20Object%5D&name=image.png&originHeight=518&originWidth=1370&size=76246&status=done&style=none&width=685)<br />2. 在 **开放平台密钥**  页面点击选择需要配置接口加签方式/接口内容加密方式的应用配置。<br />两个入口选择其一即可完成配置，详细说明可查看 [设置接口加签方式](https://opendocs.alipay.com/common/02kipl)、[设置接口内容加密方式](https://opendocs.alipay.com/common/02mse3)。<br />3. 检查设置完成后，点击 小程序右上角三个点 > 关于 > 右上角（设置）> 用户信息，解除授权后重新授权获取。<br /> |
|  |  | 缺少加密配置 |  |
|  | 40002 | 加密异常 | <br />1. 重新 [设置接口内容加密方式](https://opendocs.alipay.com/common/02mse3)（设置方式同40001）。<br />2. 检查设置完成后，点击 小程序右上角三个点 > 关于 > 右上角（设置）> 用户信息，解除授权后重新授权获取。<br /> |
| [my.navigateTo](https://opendocs.alipay.com/mini/api/zwi8gx) | 1 | depth can not be more than 10 | 页面跳转层级深度不能超过 10 层，请合理使用其它路由 API 配合来做跳转逻辑。 |
|  |  | can not find page:pages/index/index when execute navigateTo for url /pages/index/index | 页面 URL 入参路径不正确导致，请检查入参是否为正确的页面路径，可在 app.json 中查看正确路径。 |
| [my.redirectTo](https://opendocs.alipay.com/mini/api/fh18ky) | 1 | can not find page:pages/index/index when execute redirectTo for url /pages/index/index | 页面 URL 入参路径不正确导致，请检查入参是否为正确的页面路径，可在 app.json 中查看正确路径。 |
| [my.reLaunch](https://opendocs.alipay.com/mini/api/hmn54z) | 1 | can not find page:pages/index/index when execute reLaunch for url /pages/index/index | 页面 URL 入参路径不正确导致，请检查入参是否为正确的页面路径，可在 app.json 中查看正确路径。 |
| [my.switchTab](https://opendocs.alipay.com/mini/api/ui-tabbar) | 1 | can not find page:pages/index/index when execute switchTab for url /pages/index/index | <br />1. 页面 URL 入参路径不正确导致，请检查入参是否为正确的页面路径，可在 app.json 中查看正确路径。<br />2. 必须跳转的标签页的路径（需在 app.json 的 tabbar 字段定义的页面）。<br />
**注意：**<br />- 标签页的第一个页面必须是首页。<br />- 路径后不能带参数。<br /> |
| [my.navigateBack](https://opendocs.alipay.com/mini/api/kc5zbx) | already top of navigation | 已经在导航栏顶部 | 已经在导航栏顶部，无法在返回。 |

