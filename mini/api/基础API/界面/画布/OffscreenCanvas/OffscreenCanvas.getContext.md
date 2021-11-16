
# 简介
**OffscreenCanvas.getContext** 返回 OffscreenCanvas 的绘制上下文。

## 使用限制
此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 入参

### string contextType
绘图上下文类型，需要与 my.createOffscreenCanvas 时传入的 type 一致。

#### contextType 合法值
| **值** | **说明** |
| --- | --- |
| webgl | webgl 类型上下文 |
| 2d | 2d 类型上下文 |


## 返回值
返回值为 [RenderingContext](https://opendocs.alipay.com/mini/01w0it)。支持获取 2D Canvas 和 WebGL Canvas 绘制上下文。
