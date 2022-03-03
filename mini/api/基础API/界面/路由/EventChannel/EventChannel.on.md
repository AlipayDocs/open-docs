
# 简介
在页面间通信中持续监听一个事件。

## 使用限制

- 版本要求基础库 [2.7.7](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 及以上，若版本较低，建议做 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码

**发起** [my.navigateTo](https://opendocs.alipay.com/mini/api/zwi8gx) **调用的页面**：

在 `my.navigateTo` 调用中的 `events` 参数挂载需要持续监听的事件：

```JavaScript
my.navigateTo({ 
  url: './opened-page',
  // 挂载监听事件
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

**通过** [my.navigateTo](https://opendocs.alipay.com/mini/api/zwi8gx) **打开的页面**：

使用 `EventChannel` 的 `on` 方法挂载需要持续监听的事件：

```JavaScript
// 通过 my.navigateTo 打开的页面
Page({
  onLoad() {
    const eventChannel = this.getOpenerEventChannel();
    eventChannel.emit('openedToOpener', {
      message: 'Hello Opener Page!'
    });
    // 挂载监听事件
    eventChannel.on('openerToOpened', data => {
      console.log(data); // { "message": "Hi Opened Page!" }
    });
  }
});
```

## 入参
入参结构为：(String eventName, Function callback)。

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| eventName | String | 是 | 需要监听的事件的名称。 |
| callback | Function | 是 | 事件监听函数。 |

