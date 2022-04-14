
# 简介
**my.offAppHide** 是取消监听小程序切后台事件的 API。

## 使用限制
- 基础库 [1.20.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.68 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 由于开发者工具版本限制，目前本 API 暂不支持在开发者工具调试和真机调试，仅支持真机预览。开发者请调至 预览 模式，在支付宝客户端扫码查看效果。
- 请勿使用 API 监听匿名函数，否则将无法关闭监听。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用
## 示例代码
### .axml 示例代码
```html
<!-- .axml-->
<button size="default" onTap="offAppHideHanlder" type="primary">关闭监听到后台</button>
```

### .js 示例代码 
```javascript
//.js
onLoad() {
    my.onAppHide(this.onAppHideHandler)
},
// 监听切换到后台方法
onAppHideHandler() {
    console.log('监听切换到后台方法')
},
// 取消监听切换到后台方法
offAppHideHanlder() {
    my.offAppHide(this.onAppHideHandler)
},
```

## 入参
Object 类型，参数如下：
| **参数** | **类型** | **描述** |
| --- | --- | --- |
| callback | Function | 小程序切后台事件的回调函数。 |

