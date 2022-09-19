# 简介

监听录音结束事件。

## 使用限制

- 基础库 [1.11.0](https://opendocs.alipay.com/mini/framework/lib) 开始支持，低版本需要做 [兼容处理](https://docs.alipay.com/mini/framework/compatibility)。
- 此 API 暂仅支持企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码

```javascript
let recorderManager = my.getRecorderManager();
recorderManager.onStop(res => {
  console.log(res.tempFilePath);
});
```

## 入参

### Function callback

录音结束事件的回调函数。

#### callback 参数

**Object res**

| **属性**     | **类型** | **说明**            |
| ------------ | -------- | -------------------- |
| tempFilePath | String   | 录音文件的临时路径。 |
| duration | Number   | 录音总时长。单位：s。<br/> **版本要求：** 客户端 10.2.90 开始支持 <br/>|
| fileSize | Number   | 录音文件大小。单位：Byte。<br/> **版本要求：** 客户端 10.2.90 开始支持 <br/> |
