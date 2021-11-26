
# 简介
SelectorQuery.context 是获取节点Context实例查询请求。目前支持 [VideoContext](https://opendocs.alipay.com/mini/006lnn) 和 [MapContext](https://opendocs.alipay.com/mini/api/mapcontext) 的获取。

## 使用限制

- 基础库 [2.7.3](https://opendocs.alipay.com/mini/01iq3i) 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

### .axml 示例代码
```html
//page.axml
<map id="map" />
```

### .js 示例代码
```javascript
//page.js
Page({
  onReady() {
    my.createSelectorQuery().select('#map').context((res) => {
			if (res && res.context) {
        const mapContext = res.context;
        mapContext.getSkew({
          success: res => {
            console.log(res.skew);
          }
        }
      }
    }).exec();
  }
});
```

## 入参

### Function callback
在执行 [SelectorQuery.exec](https://opendocs.alipay.com/mini/api/baz2hg) 方法后执行，返回节点信息。

#### 回调参数
Object

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| context | Object | 节点对应的 Context 实例。 |

