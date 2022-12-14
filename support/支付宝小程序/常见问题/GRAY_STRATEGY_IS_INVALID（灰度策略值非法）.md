## 错误码
GRAY_STRATEGY_IS_INVALID（灰度策略值非法）。

## 错误描述
调用alipay.open.mini.version.gray.online(小程序灰度上架)时报错：GRAY_STRATEGY_IS_INVALID（灰度策略值非法）。

## 涉及接口
[alipay.open.mini.version.gray.online](https://opendocs.alipay.com/mini/03l3ev)（小程序灰度上架）

## 报错原因
传入的 gray_strategy 不合法。

## 解决方案
gray_strategy 仅支持 p10、p30、p50 三种策略值。
