在使用 **网络 API** 时，需要注意以下问题。

# 服务器域名白名单

服务器域名白名单是为了保证用户安全，所做的限制性措施，使用方法如下：

- 请登录 [开放平台控制台](https://open.alipay.com/dev/workspace) > 点击要配置的小程序，进入小程序详情页 > **设置** > **开发设置** > **服务器域名白名单** 中配置域名白名单。小程序在以下 API 调用时只能与白名单中的域名进行通讯：HTTP 请求（my.request）、上传文件（my.uploadFile）。

![|723x75](https://mdn.alipayobjects.com/afts/img/A*xM4NR6VRbfzGJmFFrCUnsgBkAa8wAA/original?bz=openpt_doc&t=LaBryvibyj5g0SshaLeFcwAAAABkMK8AAAAA#align=left&display=inline&height=168&margin=%5Bobject%20Object%5D&originHeight=168&originWidth=1624&status=done&style=stroke&width=1624)

添加服务器域名白名单后，需要重新打包上传生成体验版，服务器域名才会生效。

- 服务器域名白名单是以一级域名进行匹配的。

```plain
假如商户有 a.com 和 b.com 两个域名，业务分别部署在
1.a.com
2.a.com
1.b.com
2.b.com
3.b.com
那么，在服务器域名白名单里面只需要配置 a.com 和 b.com 即可，这里是一级域名匹配。
```

# 跳过域名检验

若在 IDE 中进行测试，请设置 **忽略 http 请求域名合法性检查**。IDE 中调试不受服务器域名白名单影响。

![|835x702](https://gw.alipayobjects.com/mdn/rms_aba389/afts/img/A*4wF6S7OPlScAAAAAAAAAAAAAARQnAQ)

# 网络请求

- 默认超时时间为 30000 ms。
- 小程序会自带 HTTP Referer，暂时不支持自定义设置 HTTP Referer。
- 只要成功接收到服务器返回，无论 status 是多少，都会进入 success 回调函数。请开发者根据业务逻辑对返回值进行判断。

# HTTPS 证书

小程序必须使用 HTTPS/WSS 发起网络请求。请求时系统会对服务器域名使用的 HTTPS 证书进行校验，如果校验失败，则请求不能成功发起。由于系统限制，不同平台对于证书要求的严格程度不同。为了保证小程序的兼容性，建议开发者按照最高标准进行证书配置，并使用相关工具检查现有证书是否符合要求。

小程序只支持 HTTPS 域名配置。 相比于 HTTP，HTTPS 可以提供更加优质保密的信息，保证了用户数据的安全性，此外 HTTPS 同时也一定程度上保护了服务端，使用恶意攻击和伪装数据的成本大幅提高。

因此小程序强制使用 HTTPS，还在使用 HTTP 协议的开发者需要尽快对服务器进行升级。
