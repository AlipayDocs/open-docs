# 简介

创建一个  Worker 线程。

## 使用限制

- 基础库 [1.11.0](https://opendocs.alipay.com/mini/framework/lib) 开始支持。若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 暂仅支持企业支付宝小程序使用。
- 目前限制最多只能创建一个 Worker，创建下一个 Worker 前请先调用  Worker.terminate。
- 使用前需要在 [app.json](https://opendocs.alipay.com/mini/framework/app-json#workers) 配置 Worker 代码文件地址。
- IDE 暂不支持此 API 调用，请在真机进行调试。

# 接口调用

## 示例代码

### app.json 示例代码

```json
{
  "workers": ["workers/request/index.js", "workers/response/index.js"]
}
```

### .js 示例代码

```javascript
const worker = my.createWorker('workers/request/index.js'); // 文件名指定 worker 的入口文件路径，绝对路径
worker.onMessage(function (res) {
  console.log(res);
});
worker.postMessage({
  msg: 'hello alipay',
});
worker.terminate();
```

## 入参

### String scriptPath

worker 入口文件的 **绝对路径**。

## 返回值

返回一个 [Worker](https://opendocs.alipay.com/mini/api/worker) 对象。
