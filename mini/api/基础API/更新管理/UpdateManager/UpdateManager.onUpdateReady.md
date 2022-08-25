
# 简介
**UpdateManager.onUpdateReady** 用于监听小程序有版本更新事件。客户端主动触发下载（无需开发者触发），下载成功后回调。

自动检查更新完成之后一段时间内会触发更新结果事件，因此请在 [App.onLaunch](https://opendocs.alipay.com/mini/framework/app-detail#onLaunch(object%3A%20Object)%20%E5%8F%8A%20onShow(object%3A%20Object)) 等较早执行的生命周期里监听该事件。onUpdateReady 注册太晚可能会导致监听不到更新结果事件。

## 使用限制
此 API 暂仅支持企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码
```javascript
// .js
const updateManager = my.getUpdateManager();
updateManager.onUpdateReady(function () {
  my.confirm({
    title: "更新提示",
    content: "新版本已经准备好，是否重启应用？",
    success: function (res) {
      if (res.confirm) {
        // 新版本已经下载好，调用 applyUpdate 应用新版本并重启
        updateManager.applyUpdate();
      }
    },
  });
});
```
