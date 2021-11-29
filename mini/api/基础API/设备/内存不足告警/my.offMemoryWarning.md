
# 简介
**my.offMemoryWarning** 是用于停止监听内存不足的告警事件的 API。

需要保证 onMemoryWarning / offMemoryWarning 中的入参（callback）是同一个对象。

## 使用限制

- 基础库 [1.11.0](https://opendocs.alipay.com/mini/framework/lib)  或更高版本；支付宝客户端 10.1.35 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。 
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验
![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/7263427976e4f3e0a8869a29c0521f44.png#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=stroke&width=127)

# 接口调用

## 示例代码
```json
{
   "defaultTitle": "OnMemoryWarning"
}
```
```html
<!-- API-DEMO page/API/memory-warning/memory-warning.axml-->
<view class="page">
  <button type="primary" onTap="onMemoryWarning">
    开始监听内存不足告警
  </button>
</view>
```
```javascript
// API-DEMO page/API/memory-warning/memory-warning.js
Page({
  onLoad() {
    this.callback = (res) => {
        var levelString = 'iOS 设备, 无 level 传入.';
        switch (res.level) {
          case 10:
            levelString = 'Android 设备, level = TRIM_MEMORY_RUNNING_LOW';
            break;
          case 15:
            levelString = 'Android 设备, level = TRIM_MEMORY_RUNNING_CRITICAL';
            break;
        }
        my.alert({
          title: '收到内存不足告警',
          content: levelString
        });
    };
    this.isApiAvailable = my.canIUse('onMemoryWarning');
  },
  onMemoryWarning() {
    if (this.isApiAvailable) {
      my.onMemoryWarning(this.callback);
    } else {
      my.alert({
        title: '客户端版本过低',
        content: 'my.onMemoryWarning() 和 my.offMemoryWarning() 需要 10.1.35 及以上版本'
      });
    }
  },
  onUnload() {
    if (this.isApiAvailable) {
      my.offMemoryWarning(this.callback); 
    }
  }
});
```

## 入参
| **属性** | **类型** | **描述** |
| --- | --- | --- |
| 回调函数 | Function | 内存不足告警事件的回调函数。 |


### 是否需要传 callback 值

- 不传递 callback 值，则会移除监听所有的事件回调。示例代码如下：
```javascript
my.offMemoryWarning();
```

- 传递 callback 值，只移除对应的 callback 事件。示例代码如下：
```javascript
my.offMemoryWarning(this.callback);
```
