
# 简介
**UpdateManager.onCheckForUpdate** 是用于监听向支付宝后台请求检查更新结果事件的 API。支付宝在小程序冷启动时自动检查更新，不需由开发者主动触发。

自动检查更新完成之后一段时间内会触发更新结果事件，因此请在 App.onLaunch 等较早执行的生命周期里监听该事件。onCheckForUpdate 注册太晚可能会导致监听不到更新结果事件。

关于小程序的更新机制，可以查看 [更新机制](https://opendocs.alipay.com/support/01rb0k) 文档。

## 使用限制
此 API 暂仅支持企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码
```javascript
// .js
const updateManager = my.getUpdateManager();
updateManager.onCheckForUpdate(function (res) {
  // 检查更新结果
  console.log(res.hasUpdate);
});
```

## 出参
Object 类型，属性如下：

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| hasUpdate | Boolean | 是 | 是否有新版本。 |

# 常见问题 FAQ

## Q：为什么我在 button 按钮上注册了一个点击回调，点击之后无法检测到更新？
A：在小程序的启动过程中会自动检测当前小程序是否有版本更新，自动检查更新完成之后一段时间内会触发更新结果事件。如果 onCheckForUpdate 事件监听执行较晚可能会接收不到更新结果事件。

