### Q：关于使用 my.redirectTo 跳转页面的页面栈深度问题
A：目前小程序中的页面栈最多为10层，可以通过 [getCurrentPages](https://opendocs.alipay.com/mini/framework/getcurrentpages) 方法 判断页面栈峰值，超过后用重定向跳转页面。
- 使用my.redirectTo跳转的页面，当页面栈深度为1时，没有返回按钮；但如果有页面层级，左上角就会出现返回按钮。
- 小程序规定最多不能超过 10 层页面栈，如果页面栈深度超过10层，从a页面跳转到b页面时，如果使用 my.navigateTo方法a页面就会被压到栈里,但不会被销毁，如果使用 my.redirectTo方法a页面就会被销毁。


### Q：使用 my.redirectTo 跳转页面时，是否可以去掉或隐藏返回按钮？
A：使用my.redirectTo跳转的页面，当页面栈深度为1时，没有返回按钮，并且右上角的按钮不能隐藏。或者可以先使用 [my.reLaunch](https://opendocs.alipay.com/mini/api/hmn54z)  进行跳转，然后使用 [my.hideBackHome](https://opendocs.alipay.com/mini/api/ui-navigate) 隐藏左上角的返回首页按钮。但是使用 **my.reLaunch** 进行跳转时，不允许跳转到 tabbar 页面。
- 如果有层级会有返回按钮。可以先调用 [my.reLaunch](https://opendocs.alipay.com/mini/api/hmn54z) 方法关闭当前打开的所有页面去跳转到此页面，然后配合使用 [my.hideBackHome](https://opendocs.alipay.com/mini/api/ui-navigate) 隐藏导航栏返回按钮。


### Q：跳转的页面为何不显示底部的 tab 栏？
A：通过页面跳转（[my.navigateTo](https://opendocs.alipay.com/mini/api/zwi8gx)）或者页面重定向（[my.redirectTo](https://opendocs.alipay.com/mini/api/fh18ky)）所到达的页面，即使它是定义在 tabBar 配置中的页面，也不会显示底部的 tab 栏。若要跳转到 tab 页面，请使用 [my.switchTab](https://opendocs.alipay.com/mini/api/ui-tabbar) 方法。
- 使用 my.redirectTo() 方法跳转到 tabBar 界面不会报错，但会触发 my.redirectTo() 的 fail 回调方法。
- 使用 my.navigateTo() 方法可以跳转到 tabBar 页面，但不会显示 tabBar。
- 使用 my.switchTab() 和 my.reLaunch() 两个方法转到 tabBar 页面才能显示 tabBar。


### Q：小程序内嵌的H5怎么跳转回小程序？
A：web-view 中可以使用路由API进行跳转，如[my.navigateTo](https://opendocs.alipay.com/mini/api/zwi8gx)、[my.redirectTo](https://opendocs.alipay.com/mini/api/fh18ky)。
-  H5 中必须引入 https://appx/web-view.min.js，否则无法调用小程序API。


### Q：my.navigateTo 或者 my.switchTab 是否支持带参数跳转？
A：my.navigateTo 支持，my.switchTab 不支持。<br />参数规则：路径与参数之间使用 `?` 分隔，参数键与参数值用 `=` 相连，不同参数必须用 `&` 分隔。<br />示例：`path?key1=value1&key2=value2` 。


### Q：my.onPageNotFound 能否处理跳转失败？
A：[my.onPageNotFound](https://opendocs.alipay.com/mini/01zdng) 和 [App.onPageNotFound](https://opendocs.alipay.com/mini/framework/app-detail#onPageNotFound(object%3A%20Object)) 只能响应小程序冷启动或热启动时的页面找不到事件。使用 [my.navigateTo](https://opendocs.alipay.com/mini/api/zwi8gx) 等路由 API 时，如果要处理目标页面不存在的场景，请使用 fail() 回调方法。
