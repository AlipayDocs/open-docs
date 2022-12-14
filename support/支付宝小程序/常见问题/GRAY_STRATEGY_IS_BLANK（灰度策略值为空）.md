## 错误码
GRAY_STRATEGY_IS_BLANK（灰度策略值为空）。

## 错误描述
调用alipay.open.mini.version.gray.online(小程序灰度上架)时报错：GRAY_STRATEGY_IS_BLANK（灰度策略值为空）。

## 涉及接口
[alipay.open.mini.version.gray.online](https://opendocs.alipay.com/mini/03l3ev)（小程序灰度上架）

## 报错原因
没有传 gray_strategy 参数。

## 解决方案
传入正确的 gray_strategy 参数灰度策略值仅支持 p10、p30、p50 三种策略。
