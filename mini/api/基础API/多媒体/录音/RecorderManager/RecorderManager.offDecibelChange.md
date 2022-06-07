# 简介

**RecorderManager.offDecibelChange** 用于取消监听声音分贝变化事件。

## 使用限制

- 使用此 API 前，请先在开放平台控制台 **创建小程序**、**添加能力**，可查看 [接入准备](https://opendocs.alipay.com/mini/02pj5u)。
- 此 API 暂仅支持企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码
```javascript
// .js
const recorderManager = my.getRecorderManager();

recorderManager.onDecibelChange((res) => {});
recorderManager.start();
setTimeout(() => {
 recorderManager.offDecibelChange();
}, 50000);
```

## 入参
| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| 回调函数 | Function | 否 | 声音分贝变化事件的回调函数。传入特定回调函数则只取消该函数的监听，不传参数则取消所有回调函数的监听。 |

