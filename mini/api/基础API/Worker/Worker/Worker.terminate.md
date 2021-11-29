
# 简介
结束当前 worker 线程，仅限在主线程 worker 对象上调用。

## 使用限制
基础库 [1.11.0](https://opendocs.alipay.com/mini/framework/lib) 开始支持，低版本需要做 [兼容处理](https://docs.alipay.com/mini/framework/compatibility)。

## 注意
Android 端的 `terminate` 方法会等待主线程 `postMessage`、worker 线程 `onMessage` 执行完毕后才真正执行。
