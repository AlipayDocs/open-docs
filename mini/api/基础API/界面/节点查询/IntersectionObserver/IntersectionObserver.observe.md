# 简介

**IntersectionObserver.observe** 用于指定目标节点并开始监听相交状态变化情况。

## 使用限制

此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 入参

入参结构为：(String targetSelector, Function callback)。

| **属性**       | **类型**          | **描述**                     |
| -------------- | ----------------- | ---------------------------- |
| targetSelector | String            | 选择器。                     |
| 回调函数       | Function callback | 监听相交状态变化的回调函数。 |

### callback 参数

**Object res 属性**

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| intersectionRatio | Number | 相交比例。 |
| intersectionRect | Object | 相交区域的边界。 |
| boundingClientRect | Object | 目标边界。 |
| relativeRect | Object | 参照区域的边界。 |
| time | Number | 相交检测时的时间戳。 |
| dataset | Object | 目标节点的 dataset 信息，使用前需要将 [my.createIntersectionObserver](https://opendocs.alipay.com/mini/api/intersectionobserver) 的 dataset 入参设置为 true。基础库 [2.7.0](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 开始支持。 |

**res.intersectionRect 属性**

| **属性** | **类型** | **描述** |
| -------- | -------- | -------- |
| left     | Number   | 左边界。 |
| right    | Number   | 右边界。 |
| top      | Number   | 上边界。 |
| bottom   | Number   | 下边界。 |

**res.boundingClientRect 属性**

| **属性** | **类型** | **描述** |
| -------- | -------- | -------- |
| left     | Number   | 左边界。 |
| right    | Number   | 右边界。 |
| top      | Number   | 上边界。 |
| bottom   | Number   | 下边界。 |

**res.relativeRect 属性**

| **属性** | **类型** | **描述** |
| -------- | -------- | -------- |
| left     | Number   | 左边界。 |
| right    | Number   | 右边界。 |
| top      | Number   | 上边界。 |
| bottom   | Number   | 下边界。 |

**res.dataset 属性**

目标节点的 dataset 信息。仅当 [my.createIntersectionObserver](https://opendocs.alipay.com/mini/api/intersectionobserver) 的 dataset 入参设置为 true 时，res 才会返回该目标节点的 dataset 属性。
