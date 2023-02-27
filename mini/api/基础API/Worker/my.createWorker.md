# 简介

创建一个 Worker 线程。

## 使用限制

- 基础库 [1.11.0](https://opendocs.alipay.com/mini/framework/lib) 开始支持。若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 暂仅支持企业支付宝小程序使用。
- IDE 暂不支持此 API 调用，请在真机进行调试。
- 目前限制最多只能创建一个 Worker，创建下一个 Worker 前请先调用 Worker.terminate。

# 接口调用

## 示例代码

### app.json
```json
{
  "workers": ["workers/index.js"]
}
```

### pages/index/index.js
```javascript
Page({
  testWorker() {
    const scriptPath = 'workers/index.js'; // worker 的入口文件
    const worker = my.createWorker(scriptPath);
    if (!worker) {
      my.alert({
        title: 'createWorker 失败',
        content: `请确保包文件路径 ${scriptPath} 有效，且在 app.json 里的 workers 数组中包含`
      });
      return;
    }
    worker.onMessage(function (msg) {
      my.alert({ title: '收到来自 worker 的消息', content: msg.text });
      worker.terminate();
    });
    worker.postMessage({
      text: 'Hello worker'
    });
  }
});
```

### workers/index.js
```javascript
worker.onMessage(function (msg) {
  worker.postMessage({
    text: msg.text + ' --- Hello master'
  });
});
```

## 入参

### String scriptPath

worker 入口文件的路径，为 [代码包文件](https://opendocs.alipay.com/mini/03dt4s#%E8%AE%BF%E9%97%AE%E4%BB%A3%E7%A0%81%E5%8C%85%E6%96%87%E4%BB%B6)（但**不支持以 "/" 开头**），需要在 app.json 中的 workers 字段中包含（参见上文示例）。

## 返回值

返回一个 [Worker](https://opendocs.alipay.com/mini/api/worker) 对象。
