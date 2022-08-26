# 简介

Worker 实例，主线程中可通过 [my.createWorker](https://opendocs.alipay.com/mini/api/createworker) 接口获取，worker 线程中可通过全局变量 `worker` 获取。

## 使用限制

基础库 [1.11.0](https://opendocs.alipay.com/mini/framework/lib) 开始支持，低版本需要做 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。

# 概览

| **名称** | **功能说明** |
| --- | --- |
| [Worker.onMessage](https://opendocs.alipay.com/mini/api/workeronmesssage) | 监听主线程/Worker 线程向当前线程发送的消息的事件。 |
| [Worker.postMessage](https://opendocs.alipay.com/mini/api/workerpostmessage) | 向主线程/Worker 线程发送的消息。 |
| [Worker.terminate](https://opendocs.alipay.com/mini/api/workerterminate) | 结束当前 worker 线程，仅限在主线程 worker 对象上调用。 |
