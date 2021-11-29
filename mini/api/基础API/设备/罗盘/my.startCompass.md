
# 简介
**my.startCompass** 开始监听罗盘数据。

## 使用限制

- 基础库 [1.24.9](https://opendocs.alipay.com/mini/framework/lib) 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码
```javascript
// page.js
Page({
  onReady() {
    this.compassChangeCallback = function (res) {
      console.log(res.direction);
    };
    my.startCompass({
      interval: 'ui',
      success: () => {
        my.onCompassChange(this.compassChangeCallback);
      }
    });
  }
})
```

## 入参
为 Object 类型。

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| interval | string | 否 | 监听罗盘数据回调函数的执行频率。默认值是<br />normal。 |
| success | function | 否 | 接口调用成功的回调函数。 |
| fail | function | 否 | 接口调用失败的回调函数。 |
| complete | function | 否 | 接口调用结束的回调函数（调用成功、失败都会执行）。 |


### object.interval 合法值
| **值** | **说明** |
| --- | --- |
| game | 适用于更新游戏的回调频率，在 20ms/次 左右。 |
| ui | 适用于更新 UI 的回调频率，在 60ms/次 左右。 |
| normal | 普通的回调频率，在 200ms/次 左右。 |

