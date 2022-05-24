# 简介
**my.reLaunch** 是关闭所有页面，跳转到应用内的某个页面。

可使用 [my.navigateBack](https://opendocs.alipay.com/mini/api/kc5zbx) 返回到原来页面。

## 使用限制

- 如果在小程序插件内调用此 API，只能跳转到此插件的页面，不能跳转到宿主页面或其他插件页面。
- 基础库 [1.4.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.8 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验

![](https://gw.alipayobjects.com/zos/skylark-tools/public/files/faba3a84de9cc461625c779a4fed1fd0.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=none&width=127)

# 接口调用

## 示例

### .js 示例代码
```javascript
Page({
  my.reLaunch({
    // 若 path 后包含特殊字符（例如 %），则需要对 path 后包含特殊字符的 key=value 参数进行 encode，否则将无法正常跳转。
    url: '/page/index?id=12&name=%22%E5%B0%8F%E6%98%8E%22&percentage=20%25'
  }, success: () => {
    console.log("跳转成功的回调");
  })
})
```

## 入参
Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| url | String | 是 | 需要跳转的应用内目标页面路径，路径后可以带参数。<br />**参数规则**：路径与参数之间使用 `?` 分隔，参数键与参数值用 `=` 相连，不同参数必须用 `&` 分隔。<br />**示例**：`path?key1=value1&key2=value2`。<br />**注意**：若 `path` 后包含特殊字符（例如 %），则需要对 `path` 后包含特殊字符的 `key=value` 参数进行 encode，否则将无法正常跳转。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

## 错误码
| **error** | **errorMessage** | **描述** |
| --- | --- | --- |
| 1 | `${url} resolved to ${pagePath} is not found` | 目标页面路径不存在 |
| 1 | `${url} is not found in plugin` | 目标页面是插件页面，但该插件并没有声明该页面 |

# 常见问题
## Q：my.navigateTo、my.redirectTo、my.reLaunch 的区别是什么？
A：三者区别在于页面层级关系的保留。   
my.navigateTo 是保留当前页面，跳转到新页面，小程序导航栏的左上角会出现 **返回上一页** 按钮。   
[my.redirectTo](https://opendocs.alipay.com/mini/api/fh18ky) 是关闭当前页面，跳转到新页面。当页面栈深度为 1 时，小程序导航栏的左上角不会出现 **返回上一页** 按钮， 当页面深度大于 1 时，会出现 **返回上一页** 按钮。   
[my.reLaunch](https://opendocs.alipay.com/mini/api/hmn54z) 是关闭所有页面，跳转到新页面，小程序导航栏的左上角会出现 **返回首页** 按钮。

## Q：如何监听小程序导航栏的左上角的 返回首页 按钮？
A：暂不支持监听小程序导航栏的左上角的 **返回首页** 按钮。

## Q：如何隐藏小程序中的导航栏的 返回首页 按钮？
A：[my.hideBackHome](https://opendocs.alipay.com/mini/api/ui-navigate) 接口可以隐藏导航栏 **返回首页** 按钮。
