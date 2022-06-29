# 简介
**my.navigateBack** 是关闭当前页面，返回上一级或多级页面的 API。可通过 [Page.getCurrentPages](https://opendocs.alipay.com/mini/framework/getcurrentpages) 获取当前的页面栈信息，决定需要返回几层。

相关问题可查看 [路由FAQ](https://opendocs.alipay.com/mini/api/fu8l65) 。


## 使用限制

此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验

![|128x158](https://cdn.nlark.com/yuque/0/2021/png/179989/1637056770503-813c17f4-e76c-4870-a0c7-5aae8768a06c.png#align=left&display=inline&height=127&margin=%5Bobject%20Object%5D&name=image.png&originHeight=157&originWidth=127&size=16714&status=done&style=none&width=103)

## 示例代码

### .json 示例代码
```json
{
  "defaultTitle": "Navigator"
}
```

### .axml 示例代码
当前页面的 .axml 示例代码：
```html
<!-- navigateBack.axml-->
<view class="page">
  <view class="page-section">
    <button type="primary" onTap="navigateBack">返回上一页</button>
    <button type="primary" onTap="navigateBackDelta">返回上一页的上一页</button>
  </view>
</view>
```
上一级页面的 .axml 示例代码：
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
当前页面的 .js 示例代码：
```javascript
// navigateBack.js
Page({
  navigateBack() {
    my.navigateBack() // 返回上一页
  },
  navigateBackDelta() {
    my.navigateBack({ delta: 2 }) // 返回上一页的上一页
  }
})
```
上一级页面的 .js 示例代码：
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

## 入参
| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| delta | Number | 否 | 返回的页面数，如果 delta 大于现有打开的页面数，则返回到首页。默认值为 1。 |

# 常见问题 FAQ

## Q：使用 my.navigateBack 返回，如何通知所到达的页面刷新？是否可以通过监听返回按钮点击或页面返回事件达到这一目的？
A：使用 my.navigateBack 返回所到达的页面并不会自动刷新。当前页面可以通过 [onBack](https://opendocs.alipay.com/mini/framework/page-detail#events) 监听到导航栏上返回按钮（以及 Android 系统返回键）被点击，但不支持监听左滑手势、API 调用等其他方式导致的返回。但无论哪种返回方式，当前页面关闭前都会触发 [onUnload](https://opendocs.alipay.com/mini/framework/page-detail#onUnload\(\))，返回到达的页面均会触发 [onShow](https://opendocs.alipay.com/mini/framework/page-detail#onShow()) ，故可利用这个机制进行必要的处理。注意 onShow 事情并不一定是通过返回触发，需要自行判断。一种实现方式如下：

```javascript

// 当前页面
Page({
  onSomeButtonTap() {
    // 在全局数据中存信息，带时间戳
    getApp().globalData.navigateBackPayload = this._navigateBackPayload = {
      time: Date.now(),
      message: 'by my.navigateBack'
    };
    // 调用接口返回
    my.navigateBack();
  },
  onUnload() {
    if (!this._navigateBackPayload) {
      // 其他方式离开页面，也存一条
      getApp().globalData.navigateBackPayload = {
        time: Date.now(),
        message: 'by other means'
      };
    }
  },
  
});

// 返回的目标页面
Page({
  onShow(options) {
    // 从全局数据中取信息
    const { globalData } = getApp();
    const { time, message } = globalData.navigateBackPayload || {};
    // 比较时间戳，推测是否为有效数据。1000ms 只是个粗糙的经验值，可调整
    if (time && Date.now() - time < 1000) {
      console.log('do something with message: ' + message);
    }
    // 清除信息，避免重复处理
    globalData.navigateBackPayload = null;
  },
});

```

## Q：my.navigateBack 是否支持跨页面传值？
A：暂不提供 API 层面的支持。开发者可以自行实现间接传值，参考上一条问题答案中的示例代码。

## Q：能否使用 my.navigateBack 退出小程序？
A：my.navigateBack 不能退出小程序，在最后一个页面调用会触发 fail 回调。退出小程序请使用 [my.exitMiniProgram](https://opendocs.alipay.com/mini/api/my.exitMiniProgram)（请注意该 API 的调用要由用户主动触发才能成功）。
