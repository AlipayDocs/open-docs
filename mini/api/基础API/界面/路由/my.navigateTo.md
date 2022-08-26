# 简介

**my.navigateTo** 保留当前页面，跳转到新页面。

跳转成功后，在目标页面使用 [my.navigateBack](https://opendocs.alipay.com/mini/api/kc5zbx) 可返回到当前页。my.navigateTo 使页面栈深度增加（最多到 10，再调没有效果），my.navigateBack 或用户返回操作使页面栈深度减小，[my.switchTab](https://opendocs.alipay.com/mini/api/ui-tabbar) 和 [my.reLaunch](https://opendocs.alipay.com/mini/api/hmn54z) 则会即关闭所有其他页面再打开目标页面，页面栈深度直接变成 1。

**注意：** 请勿使用 my.navigateTo 跳转到 tabBar 页面（app.json 中 tabBar.items 中列举的页面），否则会导致非预期的行为（如底部 tab bar 不显示）。如需跳转 tabBar 页面，请使用 [my.switchTab](https://opendocs.alipay.com/mini/api/ui-tabbar)。

## 使用限制

- 小程序中页面栈最多十层，超过十层会无法跳转。
- 如果在小程序插件内调用此 API，只能跳转到此插件的页面，不能跳转到宿主页面或其他插件页面。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验

![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/dd2c5503ee803648fc67e316760d2fb4.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=none&width=127)

# 接口调用

## 示例

[小程序在线](https://opendocs.alipay.com/openbox/mini/opendocs/navigator?view=preview&defaultPage=pages/index/index&defaultOpenedFiles=pages/index/index&theme=light)

### .js 示例代码

```javascript
// navigateTo.js
Page({
  navigateTo() {
    my.navigateTo({ url: './back' });
  },
  redirectTo() {
    my.redirectTo({ url: './back' });
  },
  reLaunch() {
    my.reLaunch({
      url: '/demo/my',
    });
  },
  switchTab() {
    my.switchTab({
      url: '/demo/my',
      success: () => {
        my.showToast({
          content: '成功',
          type: 'success',
          duration: 4000,
        });
      },
    });
  },
});
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
    },
  },
  success(res) {
    // 通过 eventChannel 向被打开页面传送数据
    res.eventChannel.emit('openerToOpened', {
      message: 'Hi Opened Page!',
    });
  },
});
```

被打开的页面可以通过 [getOpenerEventChannel](https://opendocs.alipay.com/mini/framework/page-detail#Page.prototype.getOpenerEventChannel) 获取两个页面间的通信通道：

```javascript
// 通过 my.navigateTo 打开的页面
Page({
  onLoad() {
    const eventChannel = this.getOpenerEventChannel();
    eventChannel.emit('openedToOpener', {
      message: 'Hello Opener Page!',
    });
    // 监听 openerToOpened 事件，获取上一页面通过 eventChannel 传送到当前页面的数据
    eventChannel.on('openerToOpened', data => {
      console.log(data); // { "message": "Hi Opened Page!" }
    });
  },
});
```

## 入参

Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| url | String | 是 | 需要跳转的应用内非 tabBar 的目标页面路径，路径后可以带参数，参数解析规则请参考 [小程序全局 / 页面参数设置以及解析细节](https://opendocs.alipay.com/mini/03durs)<br>如需跳转到 tabBar 页面，请使用 [my.switchTab](https://opendocs.alipay.com/mini/api/ui-tabbar) |
| events | Object | 否 | 定义页面间通信的事件监听，用于接受被打开页面传送的数据。基础库 [2.7.7](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 起支持。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

### Function success

success 回调函数会收到一个 Object 类型的对象，其属性如下：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| eventChannel | [EventChannel](https://opendocs.alipay.com/mini/api/eventchannel) | 和被打开页面进行通信。基础库 [2.7.7](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2)起支持。 |

## 错误码

fail 回调函数会收到一个 Object 类型的对象，其 error 属性为错误码，errorMessage 属性为错误消息。

<table>
  <tr>
    <th>error</th>
    <th>errorMessage</th>
    <th>描述</th>
  </tr>
  <tr>
    <td rowspan="2" align="center" >1</td>
    <td><code>${url} resolved to ${pagePath} is not found</code></td>
    <td>目标页面路径不存在。</td>
  </tr>
  <tr>
    <td><code>${url} is not found in plugin</code></td>
    <td>目标页面是插件页面，但该插件并没有声明该页面。</td>
  </tr>
</table>

# 常见问题

## Q：小程序多次通过 my.navigateTo 跳转，尝试几次后为何再点击不会跳转了？

A：小程序中页面栈深度限制为 10。可通过 [getCurrentPages](https://opendocs.alipay.com/mini/framework/getcurrentpages) 判断页面栈深度。使用 [my.redirectTo](https://opendocs.alipay.com/mini/api/fh18ky) 不会增加页面栈深度，但跳转后无法返回到当面页，使用时请综合考虑。

## Q：my.navigateTo、my.redirectTo、my.reLaunch 的区别是什么？

A：三者区别在于页面层级关系的保留。

- my.navigateTo 是保留当前页面，跳转到新页面，页面栈深度加 1。
- [my.redirectTo](https://opendocs.alipay.com/mini/api/fh18ky) 是关闭当前页面，跳转到新页面，不改变页面栈深度。
- [my.reLaunch](https://opendocs.alipay.com/mini/api/hmn54z) 是关闭所有页面，跳转到新页面，即将页面栈深度置为 1。

当页面栈深度为 1 时，小程序导航栏上没有 **返回上一页按钮**，通常会有 **返回首页** 按钮（如果当前不在首页）；当页面栈深度大于 1 时，**返回上一页按钮** 出现，**返回首页按钮** 隐藏。

## Q：如何监听小程序导航栏的左上角的 返回上一页 按钮 或 返回首页 按钮？

A：暂不支持监听小程序导航栏的左上角的 **返回上一页** 按钮 或 **返回首页** 按钮。

## Q：如何隐藏小程序导航栏左侧的 返回上一页按钮 或 返回首页按钮？

A，**返回上一页按钮** 的显示与否，由小程序框架根据页面栈深度决定，不提供直接隐藏的接口。如需要达到隐藏的效果，可使用 [my.reLaunch](https://opendocs.alipay.com/mini/api/hmn54z) 进行跳转，然后使用 [my.hideBackHome](https://opendocs.alipay.com/mini/api/ui-navigate) 隐藏左上角的返回首页按钮。

## Q：使用 my.navigateTo 或者 my.redirectTo 跳转的不显示底部的 tab bar，怎么办？

A：若要跳转到 app.json 中 tabBar.items 中列举的页面 ，请使用 [my.switchTab](https://opendocs.alipay.com/mini/api/ui-tabbar) 跳转，可正常显示 tab bar。
