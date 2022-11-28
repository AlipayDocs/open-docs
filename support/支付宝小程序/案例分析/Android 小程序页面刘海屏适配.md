屏幕刘海属于状态栏 statusbar。如果使用透明标题栏的业务（如开发者[自定义标题栏](https://opendocs.alipay.com/support/01rb0y)），屏幕刘海部分可能会导致页面顶部展示不全此时可以通过 User-Agent 判断是否是刘海屏，然后做适配。<br />
**注意**：User-Agent 支持支付宝客户端 [10.1.22](https://opendocs.alipay.com/mini/framework/lib) 及以上版本。<br />
通过 `true isConcaveScreen/true` 判断是否是刘海屏，true 为是，false 为否。

- 普通屏 User-Agent：<br />
```
"Mozilla/5.0 (Linux; U; Android 7.1.1; zh-CN; ONEPLUS A5000 Build/NMF26X) AppleWebKit/537.36 (KHTML, like Gecko) Version/4.0 Chrome/40.0.2214.89 UCBrowser/11.6.4.950 UWS/2.11.1.49 Mobile Safari/537.36 UCBS/2.11.1.49_180322095406 NebulaSDK/1.8.100112 Nebula AlipayDefined(nt:WIFI,ws:411|0|2.625) AliApp(AP/10.1.22.041066) AlipayClient/10.1.22.041066 Language/zh-Hans useStatusBar/true isConcaveScreen/false"
```

- 刘海屏（凹屏）User-Agent：<br />
```
"Mozilla/5.0 (Linux; U; Android 7.1.1; zh-CN; ONEPLUS A5000 Build/NMF26X) AppleWebKit/537.36 (KHTML, like Gecko) Version/4.0 Chrome/40.0.2214.89 UCBrowser/11.6.4.950 UWS/2.11.1.49 Mobile Safari/537.36 UCBS/2.11.1.49_180322095406 NebulaSDK/1.8.100112 Nebula AlipayDefined(nt:WIFI,ws:411|0|2.625) AliApp(AP/10.1.22.041066) AlipayClient/10.1.22.041066 Language/zh-Hans useStatusBar/true isConcaveScreen/true"
```
