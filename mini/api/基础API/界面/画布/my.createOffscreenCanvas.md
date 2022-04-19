# 简介
**my.createOffscreenCanvas** 创建离屏 Canvas 实例。

## 使用限制

- 基础库 [2.7.3](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 开始支持，低版本需做 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 入参

Object 类型，参数如下：

| **参数** | **类型** | **必填** | **说明** |
| --- | --- | --- | --- |
| width | Number | 否 | 画布宽度。默认为 100。 |
| height | Number | 否 | 画布高度。默认为 100。 |
| type | String | 否 | 创建离屏 canvas 类型（2d/webgl）。</br>可选值：</br><ul><li>2d：2d 类型上下文。</li><li>webgl：webgl 类型上下文。</li></ul> |

## 返回值
可查看 [OffscreenCanvas](https://opendocs.alipay.com/mini/021yfb)。
