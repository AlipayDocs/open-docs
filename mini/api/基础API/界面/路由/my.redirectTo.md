# 简介

**my.redirectTo** 关闭当前页面，打开指定页面。

当前页面会的“历史记录”会被抹除，即不能使用 my.navigateBack() 返回，类比浏览器中的 location.replace()。

**注意：** 请勿使用 my.redirectTo() 跳转 app.json 里 tarBar.items 中列举的页面（后文称 **tabBar 页面**），否则会有非预期的表现（底部 tab bar 不显示、左上角 返回首页 按钮不显示）。如需跳转 tabBar 页面，请使用 [my.switchTab()](https://opendocs.alipay.com/mini/api/ui-tabbar)。


## 使用限制
- 在小程序插件内调用此 API 只能跳转到此插件的页面，不能跳转到宿主页面或其他插件页面。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。


# 接口调用

## 示例

### .js 示例代码
```javascript
my.redirectTo({
  url: '/pages/hello/hello?count=100' // 也可使用相对路径，如 ../../hello/hello
})
```

## 入参

Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| url | String | 是 | 需要跳转的目标非 tabBar 页面路径，路径后可以带参数（参数解析规则可参考[小程序全局 / 页面参数设置以及解析细节](https://opendocs.alipay.com/mini/03durs)）。<br>如果目标页面是 tarBar 页面（即 app.json 里 tarBar.items 中列举的页面），请使用  [my.switchTab](https://opendocs.alipay.com/mini/api/ui-tabbar) 。  |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

## 错误码

注：fail 回调函数参数的 error 属性为错误码，errorMessage 为错误消息。

<table>
  <tr>
    <th>error</th>
    <th>errorMessage</th>
    <th>描述</th>
  </tr>
  <tr>
    <td rowspan="2">1</td>
    <td><code>${url} resolved to ${pagePath} is not found</code></td>
    <td>目标页面路径不存在。</td>
  </tr>
  <tr>
    <td><code>${url} is not found in plugin</code></td>
    <td>目标页面是插件页面，但该插件并没有声明该页面。</td>
  </tr>
</table>


# 常见问题 FAQ

## Q：my.navigateTo、my.redirectTo、my.reLaunch 的区别是什么？
A：三者区别在于页面层级关系的保留。   

- my.navigateTo 是保留当前页面，跳转到新页面，页面栈深度加 1。
- [my.redirectTo](https://opendocs.alipay.com/mini/api/fh18ky) 是关闭当前页面，跳转到新页面，不改变页面栈深度。
- [my.reLaunch](https://opendocs.alipay.com/mini/api/hmn54z) 是关闭所有页面，跳转到新页面，即将页面栈深度置为 1。

当页面栈深度为 1 时，小程序导航栏上没有 **返回上一页按钮**，通常会有 **返回首页** 按钮（如果当前不在首页）；当页面栈深度大于 1 时，**返回上一页按钮** 出现，**返回首页按钮** 隐藏。

## Q：使用 my.redirectTo 跳转的页面为何不显示底部的 tab bar ？
A：若要跳转到 app.json 中 tabBar.items 中列举的页面 ，请使用 [my.switchTab](https://opendocs.alipay.com/mini/api/ui-tabbar) 跳转，可正常显示 tab bar。

## Q：如何隐藏小程序导航栏左侧的 返回上一页按钮 或 返回首页按钮？
A，**返回上一页按钮** 的显示与否，由小程序框架根据页面栈深度决定，不提供直接隐藏的接口。如需要达到隐藏的效果，可使用 [my.reLaunch](https://opendocs.alipay.com/mini/api/hmn54z) 进行跳转，然后使用 [my.hideBackHome](https://opendocs.alipay.com/mini/api/ui-navigate) 隐藏左上角的返回首页按钮。


更多相关问题可查看 [路由FAQ](https://opendocs.alipay.com/mini/api/fu8l65) 。
