# 简介
**my.navigateTo** 保留当前页面，跳转到应用内的某个页面。

可使用 [my.navigateBack](https://opendocs.alipay.com/mini/api/kc5zbx) 返回到原来页面。

## 使用限制

- my.navigateTo 不允许跳转到选项卡（tabbar）页面，若需跳转到 tabbar 页面，请使用 [my.switchTab](https://opendocs.alipay.com/mini/api/ui-tabbar)。
- 小程序中页面栈最多十层，超过十层会无法跳转。   
- 如果在小程序插件内调用此 API，只能跳转到此插件的页面，不能跳转到宿主页面或其他插件页面。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验

![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/dd2c5503ee803648fc67e316760d2fb4.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=none&width=127)

# 接口调用

## 示例

### .axml 示例代码
```html
<!-- navigateTo.axml-->
<view class="page">
  <view class="page-section">
    <button type="primary" onTap="navigateTo">保留当前页面，跳转到新页面</button>
    <button type="primary" onTap="redirectTo">关闭当前页面，跳转到新页面</button>
    <button type="primary" onTap="reLaunch">关闭所有页面，跳转到新页面</button>
    <button type="primary" onTap="switchTab">跳转到tabbar页面“我的”，并关闭其他所有非 tabBar 页面</button>
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
通过 my.navigateTo 打开一个页面时，可以通过 `events` 监听从被打开页面发来的事件，以及通过 `success` 回调获得页面间的通信通道。
```javascript
my.navigateTo({ 
  url: './opened-page',
  events: {
  // 为指定事件添加一个监听器，获取被打开页面传送到当前页面的数据
    openedToOpener(data) {
      console.log(data); // { "message": "Hello Opener Page!" }
    }
  },
  success(res) {
  // 通过 eventChannel 向被打开页面传送数据
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
    // 监听 openerToOpened 事件，获取上一页面通过 eventChannel 传送到当前页面的数据
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
| url | String | 是 | 需要跳转的应用内非 tabbar 的目标页面路径，路径后可以带参数。带参数时请参考[小程序全局 / 页面参数设置以及解析细节](https://opendocs.alipay.com/mini/03durs)|
| events | Object | 否 | 定义页面间通信的事件监听，用于接受被打开页面传送的数据。基础库 [2.7.7](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 起支持。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

### Function success
success 回调函数会携带一个 Object 类型的对象，其属性如下：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| eventChannel | [EventChannel](https://opendocs.alipay.com/mini/api/eventchannel) | 和被打开页面进行通信。基础库 [2.7.7](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2)起支持。 |


## 错误码
| **error** | **errorMessage** | **描述** |
| --- | --- | --- |
| 1 | `${url} resolved to ${pagePath} is not found` | 目标页面路径不存在 |
| 1 | `${url} is not found in plugin` | 目标页面是插件页面，但该插件并没有声明该页面 |
| 1 | `${url} resolved to ${pagePath} is tab, which is not valid` | my.navigateTo 不允许跳转到选项卡（tabbar）页面，请使用 [my.switchTab](https://opendocs.alipay.com/mini/api/ui-tabbar) |

# 常见问题
## Q：如何在跳转后的页面接收 my.navigateTo 的 url 属性传的参数？
A：请参考[小程序全局 / 页面参数设置以及解析细节](https://opendocs.alipay.com/mini/03durs)。

## Q：小程序多次通过 my.navigateTo 跳转，尝试几次后为何再点击不会跳转了？
A：小程序中页面栈最多十层，超过十层会无法跳转。建议通过 [getCurrentPages](https://opendocs.alipay.com/mini/framework/getcurrentpages) 方法判断页面栈峰值，超过后用重定向接口 [my.redirectTo](https://opendocs.alipay.com/mini/api/fh18ky) 跳转页面。

## Q：my.navigateTo、my.redirectTo、my.reLaunch 的区别是什么？
A：三者区别在于页面层级关系的保留。   
my.navigateTo 是保留当前页面，跳转到新页面，小程序导航栏的左上角会出现 **返回上一页** 按钮。   
[my.redirectTo](https://opendocs.alipay.com/mini/api/fh18ky) 是关闭当前页面，跳转到新页面。当页面栈深度为 1 时，小程序导航栏的左上角不会出现 **返回上一页** 按钮， 当页面深度大于 1 时，会出现 **返回上一页** 按钮。   
[my.reLaunch](https://opendocs.alipay.com/mini/api/hmn54z) 是关闭所有页面，跳转到新页面，小程序导航栏的左上角会出现 **返回首页** 按钮。

## Q：如何监听小程序导航栏的左上角的 返回上一页 按钮 或 返回首页 按钮？
A：暂不支持监听小程序导航栏的左上角的 **返回上一页** 按钮 或 **返回首页** 按钮。

## Q：如何隐藏小程序中的导航栏的 返回上一页 按钮？
A：无法直接隐藏小程序导航栏的 **返回上一页** 按钮，但是可以参考以下方案达到隐藏效果：   
先调用 [my.reLaunch](https://opendocs.alipay.com/mini/api/hmn54z) 方法关闭当前所有页面去跳转到新页面，此时小程序导航栏不出现 **返回上一页** 按钮，但是会出现 **返回首页** 按钮。这时配合使用 [my.hideBackHome](https://opendocs.alipay.com/mini/api/ui-navigate) 隐藏导航栏 **返回首页** 按钮，即可达到隐藏效果。
