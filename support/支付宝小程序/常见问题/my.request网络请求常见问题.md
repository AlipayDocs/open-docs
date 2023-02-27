
## 错误码描述
下表是 my.request 网络请求 fail 回调函数返回错误码相关描述/处理。

| **fail返回错误码** | **描述/处理** |
| :--- | :--- |
| error: 1 | {error: 1, message: "not implemented!"} 请求没有结束，就跳转到了另一个页面。建议请求完成后在进行页面跳转。 |
| error: 2 | 表示请求参数错误，建议检查请求时传递的数据是否正常，格式是否正确，可以在请求前打印下入参数据日志。<br />说明：链接过长也会导致报错 error:2，建议参数放在 data 中处理。 |
| error: 11 | 表示无权跨域调用，检查请求域名是否添加了域名白名单，开发版测试可以点击IDE右上角-详情-勾选 **忽略 httpRequest **域名合法性检查。<br />注意：版本上架，一定要添加服务器域名白名单，否正会出现异常。 |
| error: 12 | 表示请求超时，建议检查网络环境是否正常，服务器是否正常响应，若请求需要时间长，可适当设置超时时间timeout。 |
| error: 13 | 表示请求超时，建议检查网络环境是否正常，服务器是否正常响应，若请求需要时间长，可适当设置超时时间timeout。 |
| error: 14 | 表示解码失败，检查前端服务端请求和响应数据格式是否一致；如：返回数据格式 text 与入参 dataType 值 JSON 不一致而导致接口报错，请修改后台返回数据格式为 JSON。 |
| error: 15 | 表示小程序页面传参如果做urlencode需要把整体参数进行编码。 |
| error: 19 | 表示 HTTP 错误，不能正常请求，请确认请求 URL 地址在外网是否能正常请求，HTTPS 协议，小程序真机上都是线上环境的正式请求，不能使用局域网本地请求。<br />（SSL 证书是否不正确，建议更换网站 SSL 证书，推荐使用 [阿里云SSL 证书](https://promotion.aliyun.com/ntms/act/sslbuy.html?utm_content=se_1005900042) 或 [Serverless云服务](https://help.aliyun.com/document_detail/121906.html)）。 |
| error: 20 | 表示请求已被停止/服务端限流，请确认请求服务器是否能正常请求和响应。 |
| error: 23 | 表示代理请求失败，建议检查代理配置是否正确。 |


## 小程序网络请求报错排查方案

1. 根据接口返回的报错信息排查，查看报错信息中error报错的错误码，根据错误码对应错误描述进行排查。错误码详情可查看 [my.request](https://opendocs.alipay.com/mini/api/owycmh#%E9%94%99%E8%AF%AF%E7%A0%81)。
2. 查看 status 的 HTTP 状态码，根据 HTTP 状态码排查具体原因。状态码对应具体信息表，请在浏览器中自行搜索。
3. 查看 errorMessage 参数中的错误信息。如果是请求格式错误，即最常见的 JSON parse data error。
   - 如果服务端可以收到请求，可以打印出小程序前端的请求数据和服务端收到的请求数据进行匹配分析。
   - 如果服务端收不到请求，请排查服务器的网络设置，是否有白名单拦截了请求或是用的网络环境是内网环境导致。

**注意：**

- 网络请求报错有众多情况导致，不同报错会有不同的信息返回，根据提示进行自查。若自查后无法解决，请联系小程序技术支持。
- HTTP 响应码 5、6 字头，是服务端问题，这个报错的根本原因是在用户的服务器上，可能是服务器配置，也可能是请求接收的问题，这边只能给出产生问题的原因是什么。无法去获取用户服务器上的信息。所以这个只能给出报错的原因是什么，可以在浏览器中试下是否可以访问这个地址能否正常访问，是否有报错，但是无法帮用户进行详细排查。

## 常见问题

### 小程序只支持HTTPS域名配置吗？
小程序只支持 HTTPS 域名配置。相比于 HTTP，HTTPS 可以提供更加优质保密的信息，保证了用户数据的安全性，此外 HTTPS 同时也一定程度上保护了服务端，使用恶意攻击和伪装数据的成本大幅提高。因此小程序强制使用 HTTPS，还在使用 HTTP 协议的开发者需要尽快对服务器进行升级。 推荐使用 [阿里云SSL 证书](https://promotion.aliyun.com/ntms/act/sslbuy.html?utm_content=se_1005900042) 或 [Serverless云服务](https://help.aliyun.com/document_detail/121906.html)。

### 如何处理my.request 请求报错[API 调用] 请配置安全域名？
此报错是未添加服务器域名白名单导致，请检查并确保已添加服务器域名白名单。

### 如何处理my.request 请求报错无权跨域调用？
可以按照以下步骤进行处理。<br />步骤一：在小程序管理中心配置服务器域名白名单。<br />步骤二：若在 IDE 中进行测试，请设置 **忽略 httpRequest** 域名合法性检查。<br />![](https://gw.alipayobjects.com/zos/workflow/workflow/202002261582714942343_75c168b671d4ce827fca23907d85f114.png#align=left&display=inline&height=523&margin=%5Bobject%20Object%5D&originHeight=796&originWidth=1142&status=done&style=none&width=750)

### my.request 请求报错 error: 19？
请确认请求URL地址在外网是否能正常请求，HTTPS 协议，小程序真机上都是线上环境的正式请求，不能使用局域网本地请求。（SSL证书是否不正确，建议更换网站 SSL 证书，推荐使用 [阿里云SSL 证书](https://promotion.aliyun.com/ntms/act/sslbuy.html?utm_content=se_1005900042) 或 [Serverless云服务](https://help.aliyun.com/document_detail/121906.html)）。

### 同时发送多个 HTTPS 请求会造成页面卡顿，每秒传输帧数（FPS）低吗？
不会的，无影响。

### 在 IDE 预览模式中测试 my.request 为何没有反应？
在IDE真机模式下，my.request 请求地址必须要使用 HTTPS 地址。

### 为什么添加服务器域名白名单不生效？
添加服务器白名单后需要重新打包上传生成体验版。

### RequestTask.abort() 方法是在小程序前端进行请求打断还是直接中止了服务端请求？
RequestTask.abort() 方法只是强制断掉了和服务端的链接，并不是阻止请求。

### my.request 请求报错 {data: "请求超时异常", error: 14, headers: {&hellip;}, status: 13, errorMessage: "JSON parse data error"} ，如何处理?
因返回数据格式 text 与入参 dataType 值 JSON 不一致而导致接口报错，请修改后台返回数据格式为 JSON。

### 小程序服务端可以从请求头部，获取到小程序 APPID 吗？
小程序服务端无法从请求头部获取到小程序 APPID。可以通过 [my.getAppIdSync](https://opendocs.alipay.com/mini/api/gazkkm) 同步获取 APPID。

### 小程序通过 my.request 访问后台，为什么后台获取不到前端 data 中携带参数的值？
建议排查后台获取参数值时，与前端携带参数的 key 是否保持一致。

### 使用 my.request 传参，为何参数出现乱码？
可以选择以下两种方法中的一种进行解决：

- 使用 POST 请求。
- 在前端使用 encodeURIComponent("你好呀") ，服务端使用 URLDecoder.decode(aa, "UTF-8") 解析。

### 为什么my.request接口设置超时时间后依旧超时？
timeout 设置超时时间，Android 会不生效（默认是30秒，不同的网络状态也不一样，wifi 15秒， 4G 20秒）后续会更新统一，具体更新请关注小程序 [更新日志](https://opendocs.alipay.com/mini/ide/framework-changelog)。

### my.request 可以同步执行吗？
my.request 是异步执行的，无法同步执行。

### 小程序网络请求支持设置 HTTP REFERER 吗？
小程序会自带 HTTP Referer，暂时不支持自定义设置 HTTP Referer。

### my.request 与 my.httpRequest 的区别是什么？

- my.request 是 my.httpRequest 的升级优化，都是小程序端与服务器端交互发起网络请求，体验上没有大的区别。
- 支付宝客户端已不再维护 my.httpRequest，建议使用 my.request。另外，钉钉客户端尚不支持 my.request。若在钉钉客户端开发小程序，则需要使用 my.httpRequest。
- my.httpRequest 的请求头默认值为 {'content-type': 'application/x-www-form-urlencoded'}。my.request 的请求头默认值为 {'content-type': 'application/json'}。此外，请求头对象里面的 key 和 value 必须是 String 类型。
- 版本要求：基础库 1.11.0 或更高版本；支付宝客户端 10.1.32 或更高版本。

### my.request 是否支持 IP 地址请求？是否支持 IPv6 域名？

- my.request 暂不支持 IP 地址请求，不支持 HTTP 请求，请使用 HTTPS 请求。
- my.request 暂不支持 IPv6 域名。
- my.request 不建议使用关于 127.0.0.1 的测试请求。

### my.request 为何显示请求失败，提示 error：2 入参有误？
链接过长导致，建议参数放在 data 中处理。

### 小程序HTTPS问题，SSL证书有免费的吗？
小程序内所有访问链接必须使用 HTTPS 协议，如果商家没有SSL证书，推荐使用 [阿里云SSL 证书](https://promotion.aliyun.com/ntms/act/sslbuy.html?utm_content=se_1005900042) 或 [Serverless云服务](https://help.aliyun.com/document_detail/121906.html)。

### 验证HTTPS的SSL证书是否可以在支付宝内使用？
可自行使用搜索引擎搜索第三方相关验证SSL证书工具进行验证。

### 为何请求接口报错N22106？
DENY_N22106("N22106"), //JSAPI_SP_Config 正则校验不通过。小程序出现 **权限调用 code: N2210**6 表示：my.request 请求域名不在白名单。

### 小程序是否支持cookie？
小程序针对服务端回设的cookie不会禁用掉，会设置到小程序进程中，下次小程序进行请求，会自动将已有的 cookie 带入到服务端请求中。前端获取不到 cookie，也不会对 cookie 做任何操作。

### 开发小程序需要向公司防火墙白名单中添加哪些域名？
小程序这边对请求不会进行转发。访问的IP就是用户的手机网络IP。没有具体域名限制。

### 开发阶段，Android 提示：Alipay-Mobile-Proxy-Server(NO_ACCESS_PRIVATE_IP1)，HTTP响应码：571。访问地址是内网IP加端口号，是什么原因导致？
iOS 和 Android 请求处理上面有所区别，不能请求到内网，请在公网可以访问的情况下请求。

### request请求，IDE上可以正确请求，真机上不可以？
首先确认是否添加了请求白名单，若已添加确认请求地址是否是是内网的地址外网无法访问。真机模拟不能使用本地IP加端口的方式请求，必须要使用外网可以访问的域名进行请求。

### 支付宝小程序的request支持设置 async:false 同步请求吗？
request请求是异步回调，不支持设置。可以用 es6 的 Promise 自行封装成同步。

### my.request()支持设置请求头referer吗？
小程序会自带 referer，暂时不支持自定义设置 referer。

### my.request Android机型报fail JSON parse data error、iOS报无效的协议？
尝试对该参数处理 data: JSON.stringify(params)。<br />检查 header 中是否传了字段名 version，version 为敏感词不能传。

### 在my.request方法中是否有类似ajax中beforeSend的函数，使用my.request的时候会产生异步操作，会先执行my.request，才执行loading，希望像ajax一样请求前可以使用beforeSend。
具体代码如下。
```xml
// request 之前就是 beforeSendmy.showLoading();
my.request({  
   complete: function () 
      {     
      my.hideLoading();
      }
});
```

### 远程调试request接口报错QHkhuZLfIVkRKCCIGzUy.js:5376 Uncaught (in promise)？
表示 Uncaught (in promise) 提示有个 JS 错误没代码捕获，是因为请求失败导致的报错，建议通过日志和工具调试器排查服务器端的请求处理。
