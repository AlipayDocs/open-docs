# 功能支持类 FAQ

## Q：tabBar 的位置是否支持设置成顶部？

A：tabBar 的位置暂不支持自定义设置。

## Q：如何监听 tabBar 点击事件？

A：在小程序页面中用 [onTabItemTap](https://opendocs.alipay.com/mini/api/navg36) 即可监听 tabBar 点击事件。

## Q：tabBar 的 icon 图标是否支持 SVG 格式？

A：不支持 SVG 格式，只支持 PNG/JPEG/JPG 图片格式。

## Q：如何设置 tab 的样式？

A：可以在 JSON 文件中直接设置样式（示例代码如下所示），或者调用 [my.setTabBarStyle](https://opendocs.alipay.com/mini/api/wcf0sv) API 进行设置。

```json
"tabBar": {
    "textColor": "#404040",
    "selectedColor": "#108ee9",
    "backgroundColor": "#F5F5F9"
  }
```

# 请求异常类 FAQ

## Q：切换 tabBar 时报错“Cannot read property 'XXX' of undefined”，如何处理？

A：切换 tabBar 时，tabBar 对应的页面中的 onLoad()、onReady()、onShow() 方法中存在某个对象访问了一个不存在的属性。

## Q：跳转页面后，为何不显示 tabBar 呢？

A：使用 [my.switchtab()](https://opendocs.alipay.com/mini/api/ui-tabbar) 和 [my.reLaunch()](https://opendocs.alipay.com/mini/api/hmn54z) 两个方法转到 tabBar 页面才能显示 tabBar。使用 [my.navigateTo()](https://opendocs.alipay.com/mini/api/zwi8gx) 或 [my.redirectTo()](https://opendocs.alipay.com/mini/api/fh18ky) ，可以跳转到 tabBar 页面，但是不会显示 tabBar。

## Q：小程序进入 tabBar 页面，如何获取上一级页面路径呢？

A：在进入页面的时候将当前页面路径存入全局，在切换 tabBar 页面的时候拿全局的地址属性即可获取上一级页面路径。
