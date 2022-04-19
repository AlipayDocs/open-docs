# 简介
**my.startPullDownRefresh** 是主动开启下拉刷新的 API。

调用 my.startPullDownRefresh 后触发下拉刷新动画，效果与用户手动下拉刷新一致（会触发 [onPullDownRefresh](https://opendocs.alipay.com/mini/006l30) 监听方法）。

当处理完数据刷新后，[my.stopPullDownRefresh](https://opendocs.alipay.com/mini/006l2x) 可停止当前页面的下拉刷新。

## 使用限制

- 本接口不受 **onPullDownRefresh** 的 `allowsBounceVertical` 、`pullRefresh` 参数影响。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验

![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/b6870cc16df411396f0c4fee0e518d6e.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=none&width=127)

# 接口调用

## Herbox

[小程序在线](https://herbox-embed.alipay.com/s/doc-pull-down-refresh?theme=light&previewZoom=75&chInfo=openhome-doc) 

## 示例代码

### .js 示例代码

```javascript
//.js
my.startPullDownRefresh()
```

## 入参
Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| success | Function | 否 | 接口调用成功的回调函数。 |
| fail | Function | 否 | 接口调用失败的回调函数。 |
| complete | Function | 否 | 接口调用结束的回调函数（调用成功、失败都会执行）。 |

