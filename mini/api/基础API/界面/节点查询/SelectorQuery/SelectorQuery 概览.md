节点查询对象类。

##  方法
| **名称** | **描述** |
| --- | --- |
| [SelectorQuery.boundingClientRect](https://opendocs.alipay.com/mini/api/na4yun) | 将当前选择节点的位置信息放入查询结果。 |
| [SelectorQuery.exec](https://opendocs.alipay.com/mini/api/baz2hg) | 将查询结果放入 Callback 回调中。 |
| [SelectorQuery.scrollOffset](https://opendocs.alipay.com/mini/api/euyxnr) | 将当前选择节点的滚动信息放入查询结果。基础库 [2.7.4](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 开始支持传入 callback 参数。可通过 `my.canIUse('createSelectorQuery.return.scrollOffset.callback')` 检测。 |
| [SelectorQuery.select](https://opendocs.alipay.com/mini/api/mwo97h) | 选择当前第一个匹配选择器的节点。 |
| [SelectorQuery.selectAll](https://opendocs.alipay.com/mini/api/aygfvh) | 选择所有匹配选择器的节点。 |
| [SelectorQuery.selectViewport](https://opendocs.alipay.com/mini/api/kwbegi) | 选择窗口对象。 |
| [SelectorQuery.node](https://opendocs.alipay.com/mini/api/node) | 获取 Node 节点实例。基础库 **2.7.0** 开始支持。 |
| [SelectorQuery.fields](https://opendocs.alipay.com/mini/api/021zn2) | 获取节点的相关信息。基础库 **2.7.3** 开始支持。<br />基础库 **2.7.4** 开始支持获取节点 id。可通过 `my.canIUse('createSelectorQuery.return.fields.object.id')` 检测。 |
| [SelectorQuery.context](https://opendocs.alipay.com/mini/api/021yfe) | 添加节点 Context 实例查询请求。目前支持 [MapContext](https://opendocs.alipay.com/mini/api/mapcontext)、[VideoContext](https://opendocs.alipay.com/mini/api/media/video/my.createvideocontext) 的获取。基础库 **2.7.3** 开始支持。 |

