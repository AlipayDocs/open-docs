# 简介

向主线程/Worker 线程发送的消息。

## 使用限制

基础库 [1.11.0](https://opendocs.alipay.com/mini/framework/lib) 开始支持，低版本需要做 [兼容处理](https://docs.alipay.com/mini/framework/compatibility)。

# 接口调用

## 示例代码

### .js 示例代码

#### worker 线程中

```javascript
// worker为全局变量
worker.postMessage({
  msg: 'hello from worker',
});
```

#### 主线程中

```javascript
const worker = my.createWorker('workers/request/index.js');
worker.postMessage({
  msg: 'hello from main',
});
```

## 入参

### Object message

需要发送的消息，必须是一个可序列化的 JavaScript 对象。
