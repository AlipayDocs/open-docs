
# 简介
**my.reLaunch** 是关闭当前所有页面，跳转到应用内的某个指定页面的 API。

相关问题请参见 [路由FAQ](/mini/api/fu8l65) 。

## 使用限制

- 基础库 [1.4.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.8 或更高版本，若版本较低，建议采取 [兼容处理](/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验
![](https://gw.alipayobjects.com/zos/skylark-tools/public/files/faba3a84de9cc461625c779a4fed1fd0.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=none&width=127)

# 接口调用

## Herbox
[小程序在线](https://herbox-embed.alipay.com/s/doc-api-navigator?theme=light&previewZoom=75&chInfo=openhome-doc) 

## 示例代码

### .js 示例代码
```javascript
// .js
my.reLaunch({
  url: '/page/index'
})
```

## 入参
Object 类型，属性如下：

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| url | String | 是 | 页面路径。如果页面不为 tabbar 页面则路径后可以带参数。<br />**参数规则**：路径与参数之间使用`?`分隔，参数键与参数值用`=`相连，不同参数必须用`&`分隔。<br />**示例**：`path?key1=value1&key2=value2` |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

