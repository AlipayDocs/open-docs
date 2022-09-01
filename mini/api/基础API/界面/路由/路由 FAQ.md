### Q：使用 my.navigateTo 或者 my.redirectTo 跳转的页面为什么不显示底部的 tab 栏？

A：通过页面跳转（[my.navigateTo](https://opendocs.alipay.com/mini/api/zwi8gx)）或者页面重定向（[my.redirectTo](https://opendocs.alipay.com/mini/api/fh18ky)）所到达的页面，即使它是定义在 tabBar 配置中的页面，也不会显示底部的 tab 栏。若要跳转到 tab 页面，请使用 [my.switchTab](https://opendocs.alipay.com/mini/api/ui-tabbar) 方法。

### Q：my.navigateTo 或者 my.switchTab 是否支持带参数跳转？

A：my.navigateTo 支持，my.switchTab 不支持。<br />参数规则：路径与参数之间使用 `?` 分隔，参数键与参数值用 `=` 相连，不同参数必须用 `&` 分隔。<br />示例：`path?key1=value1&key2=value2` 。

### Q：使用 my.redirectTo 跳转页面，是否可以去掉左上角的返回按钮？

A：当页面栈深度为 1 时，使用 [my.redirectTo](https://opendocs.alipay.com/mini/api/fh18ky) 跳转页面的左上角不会有返回按钮。

- 建议通过 [getCurrentPages 方法](https://opendocs.alipay.com/mini/framework/getcurrentpages) 判断页面栈峰值。<br />
- 或者可以直接使用 [my.reLaunch](https://opendocs.alipay.com/mini/api/hmn54z) 进行跳转，然后使用 [my.hideBackHome](https://opendocs.alipay.com/mini/api/ui-navigate) 隐藏左上角返回首页按钮。使用 **my.reLaunch** 进行跳转时，不允许跳转到 tabbar 页面。

### Q：小程序多次通过 my.navigateTo 跳转，尝试几次后为何再点击不会跳转了？

A：小程序规定最多不能超过 10 层页面栈，建议通过 [getCurrentPages](https://opendocs.alipay.com/mini/framework/getcurrentpages) 方法判断页面栈峰值，超过后用重定向跳转页面。

### Q：小程序中的导航栏返回按钮是否能隐藏？

A：因为有层级的原因，所以会有返回按钮。可以先调用 [my.reLaunch](https://opendocs.alipay.com/mini/api/hmn54z) 方法关闭当前所有页面去跳转到此页面，然后配合使用 [my.hideBackHome](https://opendocs.alipay.com/mini/api/ui-navigate) 隐藏导航栏返回按钮。

### Q：my.onPageNotFound 能否处理跳转失败？

A：[my.onPageNotFound](https://opendocs.alipay.com/mini/01zdng) 和 [App.onPageNotFound](<https://opendocs.alipay.com/mini/framework/app-detail#onPageNotFound(object%3A%20Object)>) 只能响应小程序冷启动或热启动时的页面找不到事件。使用 [my.navigateTo](https://opendocs.alipay.com/mini/api/zwi8gx) 等路由 API 时，如果要处理目标页面不存在的场景，请使用 fail() 回调方法。
