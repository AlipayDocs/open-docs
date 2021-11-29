**UpdateManager** 对象，用来管理更新，可通过 my.getUpdateManager API 获取实例。

## 使用场景
小程序上架迭代版本时，通常会遇到由于小程序的更新机制并不会立即生效、导致不能及时更新最新版本，需要开发者集成使用更新管理功能，调用 `my.getUpdateManager` 来管理更新小程序版本，参考 [my.getUpdateManager](https://opendocs.alipay.com/mini/api/zdblqg)。

## 方法
| **名称** | **描述** |
| --- | --- |
| [UpdateManager.applyUpdate](api/neau2a) | 当小程序新版本下载完成后（即收到 `onUpdateReady` 回调），强制小程序重启并使用新版本。 |
| [UpdateManager.onCheckForUpdate](api/nm7dtb) | 监听向支付宝后台请求检查更新结果事件。 |
| [UpdateManager.onUpdateReady](api/gfz316) | 监听小程序有版本更新事件。 |
| [UpdateManager.onUpdateFailed](api/sy1k0e) | 监听小程序更新失败事件。 |


## 示例代码
```javascript
const updateManager = my.getUpdateManager()
updateManager.onCheckForUpdate(function (res) {
  // 请求完新版本信息的回调
  console.log(res.hasUpdate)
})
updateManager.onUpdateReady(function () {
  my.confirm({
    title: '更新提示',
    content: '新版本已经准备好，是否重启应用？',
    success: function (res) {
      if (res.confirm) {
        // 新的版本已经下载好，调用 applyUpdate 应用新版本并重启
        updateManager.applyUpdate()
      }
    }
  })
})
updateManager.onUpdateFailed(function () {
  // 新版本下载失败
})
```
