# 简介
监听录音错误事件。

## 使用限制

- 基础库 [1.11.0](https://opendocs.alipay.com/mini/framework/lib) 开始支持，低版本需要做 [兼容处理](https://docs.alipay.com/mini/framework/compatibility)。
- 此 API 暂仅支持企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码
```javascript
let recorderManager = my.getRecorderManager();
recorderManager.onError(res => {
 console.log(res);
})
```

## 入参

### Function callback
录音错误事件的回调函数。

#### callback 参数
**Object res**

| **属性** | **类型** | **说明** |
| --- | --- | --- |
| error | Number | 错误码。 |
| errMsg | String | 错误信息。 |

**错误码描述**

| **error** | **说明** |
| --- | --- |
| 10 | 获取权限失败 |
| 2 | 参数无效 |
| -1	 | 编码器创建失败 |
| -3 | 参数校验失败 |
| -4 | 已有录制在进行 |
| -5 | 录制被打断 |
| -6 | 系统队列开始失败 |
| -7 | 时间不足 1s |
| -8 | 系统队列创建失败 |
