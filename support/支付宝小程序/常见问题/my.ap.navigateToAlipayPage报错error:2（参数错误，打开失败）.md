## 错误码
2

## 报错描述
my.ap.navigateToAlipayPage 打开跳转到支付宝官方业务或运营活动页面报错 error:2（参数错误，打开失败）。

## 涉及接口
[my.ap.navigateToAlipayPage](https://opendocs.alipay.com/mini/api/navigatetoalipaypage)

## 报错原因
跳转到支付宝官方业务或运营活动页面链接有误、跳转的链接无权限。

## 解决方案

- 建议检查 H5 页面链接地址 scheme 或 url 是否有误，可以修改错误 H5 页面链接。
- appCode 入参是否有空格、填写正确，参数值必须为文档提供的跳转场景值。
- path 和 appCode 二选一，必填。
- 可跳转域名以 `https://render.alipay.com/p` 开头的支付宝业务、运营页面（生活号文章链接等）。部分支付宝运营、业务页面目前暂不开放跳转。
