# 简介

**IntersectionObserver.relativeTo** 是使用选择器指定一个节点，作为参照区域之一。

## 使用限制

此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 入参

入参结构为：(String selector,Object margins) String selector，选择器。 Object margins，用来扩展（或收缩）参照节点布局区域的边界，属性如下：

| **属性** | **类型** | **必填** | **描述**               |
| -------- | -------- | -------- | ---------------------- |
| left     | Number   | 否       | 节点布局区域的左边界。 |
| right    | Number   | 否       | 节点布局区域的右边界。 |
| top      | Number   | 否       | 节点布局区域的上边界。 |
| bottom   | Number   | 否       | 节点布局区域的下边界。 |
