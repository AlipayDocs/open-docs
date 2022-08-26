一些后台系统有 ip 访问限制，比如：“alipay-dev 访问支付宝这边的网络信息，主要是域名或 ip，以及对应的端口。这边 CI 流水线访问外网需申请白名单。”

miniu 的 ip 访问域名如下，请开发者需确认以下域名列入白名单，才可确保正常使用。

- ideservice.alipay.com
- gw.alipayobjects.com（对于使用本地编译真机预览会使用到）
- hpmweb.alipay.com (真机调试会会用到)
