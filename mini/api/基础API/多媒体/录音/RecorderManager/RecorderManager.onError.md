# 简介

监听录音错误事件。

## 使用限制

- 基础库 [1.11.0](https://opendocs.alipay.com/mini/framework/lib) 开始支持，低版本需要做 [兼容处理](https://docs.alipay.com/mini/framework/compatibility)。
- 小程序开发者工具（IDE）暂不支持调试此 API，请以真机调试结果为准。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码

```javascript
let recorderManager = my.getRecorderManager();
recorderManager.onError(res => {
  console.log(res);
});
```

## 入参

### Function callback

录音错误事件的回调函数。

#### callback 参数

**Object res**

| **属性** | **类型** | **说明**   |
| -------- | -------- | ---------- |
| error    | Number   | 错误码。   |
| errMsg   | String   | 错误信息。 |

**错误码描述**

| **error** | **errMsg**         |  **解决方案**|**平台** |
| --------- | ---------------- | --------- | --------- | 
| 2         | 参数无效。         | 请检查入参是否有效。   | Android  | 
| 3         | 参数校验失败。  |  请检查入参是否合理，不合理的入参会导致编码器不能识别从而报错。<br />注意：如有传入采样率与编码码率，请确保两个参数区间对应关系是正确的，否则也会报此错误。 |Android  | 
| 8607 / 8507         | 参数校验失败。  |  请检查入参是否合理，不合理的入参会导致编码器不能识别从而报错。<br />注意：如有传入采样率与编码码率，请确保两个参数区间对应关系是正确的，否则也会报此错误。 |iOS  |
| 4         | 已有录制在进行。      |  当前已有录制在进行，可在交互设计中考虑这种情况。  |Android  | 
| 8607         | 已有录制在进行。         | 当前已有录在进行，可在交互设计中考虑这种情况。   |  iOS  |
| 7         | 时间不足1s。         |  请保证录音时长超过 1s，可在交互设计中考虑这种情况。| Android  |
| 10        | 获取权限失败。   |   为用户拒绝行为，可以调用 [my.showAuthGuide](https://opendocs.alipay.com/mini/api/show-auth-guide) 引导用户开启相关系统权限。  |Android、iOS  |
| 1001         | 录制被打断。         |  录音被打断，可在交互设计中考虑这种情况。  | Android、iOS  |

