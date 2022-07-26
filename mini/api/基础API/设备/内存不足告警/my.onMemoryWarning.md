# 简介
**my.onMemoryWarning** 是用于开始监听内存不足的告警事件的 API。

## 使用限制

- Android 有告警等级划分：TRIM_MEMORY_RUNNING_LOW 和 TRIM_MEMORY_RUNNING_CRITICAL；iOS 无等级划分。
- 基础库 [1.11.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.35 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验
![](https://gw.alipayobjects.com/zos/skylark-tools/public/files/a6f461053a655a19f17b671c94ddefaa.png#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=none&width=127)

# 接口调用

## 示例
[小程序在线](https://opendocs.alipay.com/openbox/mini/opendocs/memory-warning?view=preview&defaultPage=pages/index/index&defaultOpenedFiles=pages/index/index&theme=light) 

### .json 示例代码
```json
{
   "defaultTitle": "OnMemoryWarning"
}
```

### .axml 示例代码
```html
<!-- API-DEMO page/API/memory-warning/memory-warning.axml-->
<view class="page">
  <button type="primary" onTap="onMemoryWarning">
    开始监听内存不足告警
  </button>
</view>
```

### .js 示例代码
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
入参为 Function(callback) 类型，callback 回调函数的参数类型为 Object 类型，属性如下：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| level | Number | 系统内存的告警等级, 仅 Android 有此字段。 |

Android 下告警等级对应系统宏：
```javascript
int TRIM_MEMORY_RUNNING_LOW = 10
int TRIM_MEMORY_RUNNING_CRITICAL = 15
```
