
# 简介
监听主线程/Worker 线程向当前线程发送的消息的事件。

## 使用限制
基础库 [1.11.0](https://opendocs.alipay.com/mini/framework/lib) 开始支持，低版本需要做 [兼容处理](https://docs.alipay.com/mini/framework/compatibility)。

# 接口调用

## 示例代码

### .js 示例代码

#### worker 线程中
```javascript
worker.onMessage(function (message) {
  console.log(message);
});
```

#### 主线程中
```javascript
const worker = my.createWorker('workers/request/index.js');
worker.onMessage(function (message) {
  console.log(message);
});
```

## 入参

### function callback
主线程/Worker 线程向当前线程发送的消息的事件的回调函数。

### callback参数
| **属性** | **类型** | **说明** |
| --- | --- | --- |
| message | Object | 主线程/Worker 线程向当前线程发送的消息。 |

