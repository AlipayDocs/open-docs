# 简介

**my.reLaunch** 是关闭所有页面，跳转到应用内的某个页面。

## 使用限制

- 如果在小程序插件内调用此 API，只能跳转到此插件的页面，不能跳转到宿主小程序页面或其他插件页面。
- 基础库 [1.4.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.8 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持支付宝个人小程序、支付宝企业小程序使用。

## 扫码体验

![](https://gw.alipayobjects.com/zos/skylark-tools/public/files/faba3a84de9cc461625c779a4fed1fd0.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=none&width=127)

# 接口调用

## 示例

[小程序在线](https://opendocs.alipay.com/openbox/mini/opendocs/navigator?view=preview&defaultPage=pages/index/index&defaultOpenedFiles=pages/index/index&theme=light)

### .js 示例代码

```javascript
Page({
  onTap() {
    my.reLaunch({
      // 特殊字符（中文等）需要 encode 处理，否则无法正常跳转
      url: `/page/index?id=12&name=${encodeURIComponent(
        '小明'
      )}&percentage=${encodeURIComponent('%')}`,
      success: () => {
        console.log('跳转成功');
      },
    });
  },
});
```

## 入参

Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| url | String | 是 | 需要跳转的应用内目标页面路径。<br />- 若跳转到 tab bar 页面，基础库 [2.8.1](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2)  开始支持传参。<br />- 若跳转到非 tab bar 页面支持传参。<br /> 路径后带参数时请查看 [如何获取各种场景的启动参数](https://opendocs.alipay.com/support/01rb2a)。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

## 错误码

<table>
  <tr>
    <th><b>error</b></th>
    <th><b>errorMessage</b></th>
    <th><b>描述</b></th>
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

# 常见问题

## Q：my.navigateTo、my.redirectTo、my.reLaunch 的区别是什么？

A：三者区别在于页面层级关系的保留。  
my.navigateTo 是保留当前页面，跳转到新页面，小程序导航栏的左上角会出现 **返回上一页** 按钮。  
[my.redirectTo](https://opendocs.alipay.com/mini/api/fh18ky) 是关闭当前页面，跳转到新页面。当页面栈深度为 1 时，小程序导航栏的左上角不会出现 **返回上一页** 按钮，当页面深度大于 1 时，会出现 **返回上一页** 按钮。  
[my.reLaunch](https://opendocs.alipay.com/mini/api/hmn54z) 是关闭所有页面，跳转到新页面，小程序导航栏的左上角会出现 **返回首页** 按钮。

## Q：如何监听小程序导航栏的左上角的 返回首页 按钮？

A：暂不支持监听小程序导航栏的左上角的 **返回首页** 按钮。

## Q：如何隐藏小程序中的导航栏的 返回首页 按钮？

A：[my.hideBackHome](https://opendocs.alipay.com/mini/api/ui-navigate) 接口可以隐藏导航栏 **返回首页** 按钮。
