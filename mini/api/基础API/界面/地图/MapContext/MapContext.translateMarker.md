# 简介

**MapContext.translateMarker** 是平移点标记（marker）接口。对同一个 markerId，在 translateMarker 没调用 animationEnd 之前再次调动无法生效，需要在调用 animationEnd 之后再调用一次动画，才会有效。

## 使用限制

- 基础库 [1.10.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.50 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 小程序开发者工具（IDE）暂不支持调试此 API，请使用 [真机调试](https://opendocs.alipay.com/mini/ide/remote-debug) 功能在真机进行调试。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码

```javascript
// .js
this.mapCtx = my.createMapContext('map');
this.mapCtx.translateMarker({
    markerId:0, // 必填
    destination:{
        longitude:120.2,latitude:30.3 // 必填
    },
    autoRotate:true, // 选填，默认true
    rotate:90,  // 选填，在autoRotate为false的情况下才有效，不填默认是0
    duration:900,  // 选填，单位ms，默认1000 ms
    animationEnd: () => {
        console.log('animation end')
    }   //function 动画结束回调    
});
```

## 入参

Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| markerId | Number | 是 | 指定 marker。 |
| destination | Object | 是 | 指定 marker 移动到的目标点。 |
| autoRotate | Boolean | 否 | 移动过程中是否自动旋转 marker。 |
| rotate | Number | 否 | marker 的旋转角度。默认值为 0。 |
| duration | Number | 否 | 动画持续时长。默认值为 1000。 |
| animationEnd | Function | 否 | 动画结束回调函数。 |
| success | Function | 否 | 接口调用成功的回调函数。 |
| fail | Function | 否 | 接口调用失败的回调函数。 |
| complete | Function | 否 | 接口调用结束的回调函数（调用成功、失败都会执行）。 |

### Object destination
| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| longitude | Number | 是 | 经度。 |
| latitude | Number | 是 | 纬度。 |

