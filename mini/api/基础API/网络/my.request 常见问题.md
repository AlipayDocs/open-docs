# 小程序网络请求报错排查方案

1. 通过接口返回的报错信息进行排查，根据报错信息 error 中的错误码对照 [my.request](https://opendocs.alipay.com/mini/api/owycmh) 的错误码表格进行排查。
2. 根据 status 的 HTTP 状态码排查具体原因。如果 HTTP 响应码以 5、6 字开头，说明是服务端问题，可能是服务器配置问题、请求接收问题，可以在浏览器中尝试这个地址能否正常访问，是否有报错。
3. 根据 errorMessage 参数中的错误信息进行排查，例如 "JSON parse data error" 为请求格式错误。
4. 如果后端服务器可以接受请求，则可通过打印出小程序前端的请求数据和后端收到的请求数据进行匹配分析来寻找错误原因。
5. 如果后端服务器不可以接受请求，请排查服务器的网络设置，查询是否有白名单拦截了请求，或是使用的网络环境是内网环境导致。

# 配置域名白名单

[域名白名单配置](https://forum.alipay.com/mini-app/post/97201034)。

添加服务器域名白名单后，需要重新打包上传生成体验版，服务器域名才会生效。

# 功能支持类 FAQ

## Q：小程序只支持 HTTPS 域名配置吗？

A：小程序只支持 HTTPS 域名配置。

## Q：my.request 同时发起的请求数量有限制吗？同时发送多个 HTTPS 请求会造成页面卡顿，每秒传输帧数（FPS）低吗？

A：my.request 同时发起的请求数量没有限制，不会造成页面卡顿、每秒传输帧数低。

## Q：小程序网络请求支持设置 HTTP Referer 吗？

A：小程序会自带 HTTP Referer，暂时不支持自定义设置 HTTP Referer。

## Q：小程序是否支持 cookie？

A：可以支持。服务端可以直接设置。前端需要开启 enableCookie 后支持（10.2.33版本后生效）。

# 请求异常类 FAQ

## Q：my.request 请求报错“[API 调用] 请配置安全域名”，如何处理？

A：此报错是未添加服务器域名白名单所致，请检查并确保已添加服务器域名白名单。

## Q：my.request 请求报错“无权跨域调用”，如何处理？

A：

- 在开放平台控制台对应小程序中配置服务器域名白名单。
- 若在 IDE 中进行测试，请设置 **忽略 http 请求域名合法性检查**。

![|835x702](https://gw.alipayobjects.com/mdn/rms_aba389/afts/img/A*wRsjRpU-WRkAAAAAAAAAAAAAARQnAQ)

## Q：添加服务器域名白名单，为什么不生效呢？

A：添加服务器白名单后需要重新打包上传生成体验版。

## Q：my.request 请求报错 "error":19，如何处理?

A：

- 请确认请求 URL 地址在外网是否能正常请求，HTTPS 协议，小程序真机上都是线上环境的正式请求，不能使用局域网本地请求。
- 一般如：HTTP 404、500、504 等异常错误，建议打开 **IDE** **调试器 > Network** 可以查看具体的错误信息，然后根据对应 HTTP 错误码对症处理。
- SSL 证书不正确导致的，建议更换网站 SSL 证书。

## Q：my.request 请求报错 {"data":"请求超时异常", "error":14, "headers": "{……}", "status":13, "errorMessage": "JSON parse data error"} ，如何处理?

A：因返回数据格式 text 与入参 dataType 值 JSON 不一致而导致接口报错，请修改后台返回数据格式为 JSON。

## Q：my.request 请求超时？

A：

- 请优先确认请求 URL 地址是否能正常请求。
- my.request 默认超时时间为 30s，上限为 60s，可根据实际业务情况设置超时时间。

## Q：苹果手机my.request 请求成功，安卓则失败？

A：

- 请确认请求的域名证书链是否完整[检测网址](https://myssl.com)。
- IOS和安卓的效验规则是不一样的。 ios系统库有证书链补全能力，android没有，所以ios能成功，android不行
