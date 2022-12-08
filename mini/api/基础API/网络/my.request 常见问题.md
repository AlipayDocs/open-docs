# 小程序网络请求报错排查方案

1. 通过接口返回的报错信息进行排查，根据报错信息 error 中的错误码对照 [my.request](https://opendocs.alipay.com/mini/api/owycmh) 的错误码表格进行排查。
2. 根据 status 的 HTTP 状态码排查具体原因。如果 HTTP 响应码以 5、6 字开头，说明是服务端问题，可能是服务器配置问题、请求接收问题，可以在浏览器中尝试这个地址能否正常访问，是否有报错。
3. 根据 errorMessage 参数中的错误信息进行排查，例如 "JSON parse data error" 为请求格式错误。
4. 如果后端服务器可以接受请求，则可通过打印出小程序前端的请求数据和后端收到的请求数据进行匹配分析来寻找错误原因。
5. 如果后端服务器不可以接受请求，请排查服务器的网络设置，查询是否有白名单拦截了请求，或是使用的网络环境是内网环境导致。

# 配置域名白名单

请登录 [开放平台控制台](https://open.alipay.com/dev/workspace) > 点击要配置的小程序，进入小程序详情页 > **开发设置** > **服务器域名白名单** 中配置域名白名单。小程序在以下 API 调用时只能与白名单中的域名进行通讯：HTTP 请求（my.request）、上传文件（my.uploadFile）。

![|723x75](https://cdn.nlark.com/yuque/0/2022/png/201640/1666859807363-3a9cdff5-e63c-42cd-885e-42a85d766183.png)

添加服务器域名白名单后，需要重新打包上传生成体验版，服务器域名才会生效。

# 功能支持类 FAQ

## Q：小程序只支持 HTTPS 域名配置吗？

A：小程序只支持 HTTPS 域名配置。

相比于 HTTP，HTTPS 可以提供更加优质保密的信息，保证了用户数据的安全性，此外 HTTPS 同时也一定程度上保护了服务端，使用恶意攻击和伪装数据的成本大幅提高。

因此小程序强制使用 HTTPS，还在使用 HTTP 协议的开发者需要尽快对服务器进行升级。

## Q：my.request 支持 Promise 风格调用吗？

A：支持。样例： my.request({url: ''}).then(res => console.log(res)).catch(err => console.log(err))
    
## Q：RequestTask.abort() 方法是在小程序前端进行请求打断还是直接中止了服务端请求？

A：RequestTask.abort() 方法只是强制断掉了和后端的链接，并不是阻止请求。

## Q：小程序后端可以从 HTTP Header，获取到小程序 APPID 吗？

A：小程序后端无法从请求头获取到小程序 APPID。可以通过 my.getAppIdSync 同步获取 APPID。

## Q：my.request 同时发起的请求数量有限制吗？同时发送多个 HTTPS 请求会造成页面卡顿，每秒传输帧数（FPS）低吗？

A：my.request 同时发起的请求数量没有限制，不会造成页面卡顿、每秒传输帧数低。

## Q：是否可以本地测试小程序请求服务端呢？

A：不可以本地测试小程序请求服务端。

## Q：my.request 可以同步执行吗？

A：my.request 是异步执行的，无法同步执行。

## Q：小程序网络请求支持设置 HTTP Referer 吗？

A：小程序会自带 HTTP Referer，暂时不支持自定义设置 HTTP Referer。

## Q：my.request 是否支持 IP 地址请求？是否支持 IPv6 域名？

A：

- my.request 暂不支持 IP 地址请求，不支持 HTTP 请求，请使用 HTTPS 请求。
- 支付宝客户端 10.2.30 或更高版本，my.request 支持 IPv6 域名。
- my.request 不建议使用关于 127.0.0.1 的测试请求。

## Q：小程序是否支持 cookie？

A：小程序针对服务端回设的 cookie 不会禁用掉，会设置到小程序进程中，下次小程序进行请求会自动将已有的 cookie 带入到服务端请求中。前端获取不到 cookie，也不会对 cookie 做任何操作。

## Q：my.request 与 my.httpRequest 的区别是什么呢？

A：

- my.request 是 my.httpRequest 的升级优化，都是小程序端与服务器端交互发起网络请求，体验上没有大的区别。
- 支付宝客户端已不再维护 my.httpRequest，建议使用 my.request。另外，钉钉客户端尚不支持 my.request。若在钉钉客户端开发小程序，则需要使用 my.httpRequest。
- my.httpRequest 的请求头默认值为 {'content-type': 'application/x-www-form-urlencoded'}。my.request 的请求头默认值为 {'content-type': 'application/json'}。此外，请求头对象里面的 key 和 value 必须是 String 类型。
- 版本要求：基础库 1.11.0 或更高版本；支付宝客户端 10.1.32 或更高版本。

# 请求异常类 FAQ

## Q：my.request 请求报错“[API 调用] 请配置安全域名”，如何处理？

A：此报错是未添加服务器域名白名单所致，请检查并确保已添加服务器域名白名单。

## Q：my.request 请求报错“无权跨域调用”，如何处理？

A：

- 在开放平台控制台对应小程序中配置服务器域名白名单。
- 若在 IDE 中进行测试，请设置 **忽略 http 请求域名合法性检查**。

![|835x702](https://gw.alipayobjects.com/mdn/rms_aba389/afts/img/A*wRsjRpU-WRkAAAAAAAAAAAAAARQnAQ)

## Q：在 IDE 预览模式中测试 my.request 为何没有反应？

A：在 IDE 中测试 my.request，需在 IDE 真机模式下，且 my.request 请求地址必须要使用 HTTPS 地址。

## Q：添加服务器域名白名单，为什么不生效呢？

A：添加服务器白名单后需要重新打包上传生成体验版。

## Q：小程序通过 my.request 访问后台，为什么后台获取不到前端 data 中携带参数的值？

A：建议排查后台获取参数值时，与前端携带参数的 key 是否保持一致。

## Q：使用 my.request 传参，为何参数出现乱码？

A：可以选择以下两种方法中的其中一种进行解决：

- 使用 POST 请求。
- 在前端使用 encodeURIComponent("你好呀") ，后端使用 URLDecoder.decode(aa, "UTF-8") 解析。

## Q：my.request 请求报错 "error":19，如何处理?

A：

- 请确认请求 URL 地址在外网是否能正常请求，HTTPS 协议，小程序真机上都是线上环境的正式请求，不能使用局域网本地请求。
- 一般如：HTTP 404、500、504 等异常错误，建议打开 **IDE** **调试器 > Network** 可以查看具体的错误信息，然后根据对应 HTTP 错误码对症处理。
- SSL 证书不正确导致的，建议更换网站 SSL 证书。

## Q：my.request 为何显示请求失败，提示 "error":2 入参有误？

A：

- 可能是链接过长导致，建议参数放在 data 中处理。
- 建议检查请求时传递的数据是否正常，格式是否正确，可以在请求前打印入参数据日志。

## Q：my.request 请求报错 {"data":"请求超时异常", "error":14, "headers": "{……}", "status":13, "errorMessage": "JSON parse data error"} ，如何处理?

A：因返回数据格式 text 与入参 dataType 值 JSON 不一致而导致接口报错，请修改后台返回数据格式为 JSON。

## Q：my.request 请求超时？

A：

- 请优先确认请求 URL 地址是否能正常请求。
- my.request 默认超时时间为 30s，上限为 60s，可根据实际业务情况设置超时时间。

## Q：本地调试时接口报错提示"error 12"或"似乎已断开与互联网的连接"？

A：请检查 App 的局域网权限是否正常。例如 iOS 系统的 **设置** 中，找到支付宝 App，确认 **本地网络** 选项是否打开。

## Q：请求接口报错 “N22106”？

A：小程序出现权限调用 code: N22106 表示：my.request 请求域名不在白名单。建议配置域名白名单。
