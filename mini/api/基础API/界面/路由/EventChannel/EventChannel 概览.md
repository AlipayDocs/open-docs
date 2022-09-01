# 简介

页面间事件通信通道。

## 使用限制

版本要求基础库 [2.7.7](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 及以上，若版本较低，建议做 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。

# 方法

| **名称** | **描述** |
| --- | --- |
| [EventChannel.emit](https://opendocs.alipay.com/mini/api/eventchannel.emit) | 触发一个事件。 |
| [EventChannel.on](https://opendocs.alipay.com/mini/api/eventchannel.on) | 持续监听一个事件。 |
| [EventChannel.once](https://opendocs.alipay.com/mini/api/eventchannel.once) | 监听一个事件一次，触发后失效。 |
| [EventChannel.off](https://opendocs.alipay.com/mini/api/eventchannel.off) | 取消监听一个事件。给出第二个参数时，只取消给出的监听函数，否则取消该事件的所有监听函数。 |
