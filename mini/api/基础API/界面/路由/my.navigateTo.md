# 简介
**my.navigateTo** 是从当前页面，跳转到应用内的某个指定页面的 API。

相关问题可查看 [路由FAQ](https://opendocs.alipay.com/mini/006l1n) 。

## 使用限制

- 可使用 [my.navigateBack](https://opendocs.alipay.com/mini/006l1j) 返回到原来页面。
- 小程序中页面栈最多十层。
- my.navigateTo 和 [my.redirectTo](https://opendocs.alipay.com/mini/006l1b) 不允许跳转到选项卡（tabbar）页面；若需跳转到 tabbar 页面，请使用 [my.switchTab](https://opendocs.alipay.com/mini/006l13)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验

![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/dd2c5503ee803648fc67e316760d2fb4.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=none&width=127)

# 接口调用

## Herbox

[小程序在线](https://herbox-embed.alipay.com/s/doc-api-navigator?theme=light&previewZoom=75&chInfo=openhome-doc) 

## 示例代码

### .json 示例代码
```json
{
    "defaultTitle": "Navigator"
}
```

### .axml 示例代码
```html
<!-- navigateTo.axml-->
<view class="page">
  <view class="page-section">
    <button type="primary" onTap="navigateTo">跳转新页面</button>
    <button type="primary" onTap="redirectTo">在当前页面打开新页面</button>
    <button type="primary" onTap="switchTab">跳转到“我的”</button>
    <button type="primary" onTap="reLaunch">重新打开</button>
  </view>
</view>
```

### .js 示例代码
```javascript
// navigateTo.js
Page({
  navigateTo() {
    my.navigateTo({ url: './back' })
  },
  redirectTo() {
    my.redirectTo({ url: './back' })
  },
  reLaunch() {
    my.reLaunch({
      url: '/demo/my',
    })
  },
  switchTab() {
    my.switchTab({
        url: '/demo/my',
        success: () => {
          my.showToast({
            content: '成功',
            type: 'success',
            duration: 4000
          });
        }
      }
    );
  },
})
```
#### 页面间通信
上一个页面通过 my.navigateTo 打开下一个页面时，可以通过 `events` 监听从下一个页面发来的事件，以及通过 `success` 回调获得页面间的通信通道。
```javascript
my.navigateTo({ 
  url: './opened-page',
  events: {
    openedToOpener(data) {
      console.log(data); // { "message": "Hello Opener Page!" }
    }
  },
  success(res) {
  	res.eventChannel.emit('openerToOpened', {
      message: 'Hi Opened Page!'
    });
  }
});
```
被打开的页面可以通过 [getOpenerEventChannel](https://opendocs.alipay.com/mini/framework/page-detail#Page.prototype.getOpenerEventChannel) 获取两个页面间的通信通道：
```javascript
// 通过 my.navigateTo 打开的页面
Page({
  onLoad() {
    const eventChannel = this.getOpenerEventChannel();
    eventChannel.emit('openedToOpener', {
      message: 'Hello Opener Page!'
    });
    eventChannel.on('openerToOpened', data => {
      console.log(data); // { "message": "Hi Opened Page!" }
    });
  }
});
```

## 入参
Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| url | String | 是 | 需要跳转的应用内非 tabbar 的目标页面路径，路径后可以带参数。<br />**参数规则**：路径与参数之间使用 `?` 分隔，参数键与参数值用 `=` 相连，不同参数必须用 `&` 分隔。<br />**示例**：`path?key1=value1&key2=value2`。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |
| events | Object | 否 | 定义页面间通信的事件（接受被打开页面的数据）。基础库 [2.7.7](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2)起支持。 |


### success 回调函数
success 回调函数会携带一个 Object 类型的对象，其属性如下：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| eventChannel | [EventChannel](https://opendocs.alipay.com/mini/02dcov) | 和被打开页面进行通信。基础库 [2.7.7 ](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2)起支持。 |

