## 报错描述
JS 中引入 SJS 报错：getRegExp is not defined 或者在 JS 文件中调用 getRegExp() 报错：getRegExp is not defined。

## 报错原因
getRegExp() 调用没有开启 component2 编译或者不是在 SJS 中调用导致。

## 解决方案

1. [getRegExp()](https://opendocs.alipay.com/mini/framework/datatype#regexp) 函数用于 SJS 自定义脚本中生成 regexp 对象使用正则；不能在 JS 文件中直接调用（JS 中可以直接 new RegExp() 生成使用正则，具体使用可以搜索引擎搜索相关资料）。

getRegExp() 使用示例：
```javascript
//生成 regexp 对象需要使用 getRegExp 函数。
getRegExp(pattern[, flags])
```
new RegExp() 使用示例（具体使用可以搜索引擎搜索相关资料）：
```
var re = new RegExp("\\\\w+");
```

2. JS 中 import 引入 SJS 调用到 getRegExp()，需要在 IDE 右上角点击 **详情** 在 **项目配置** 中勾选 **启用 component2 编译**。![](https://gw.alipayobjects.com/zos/workflow/workflow/202003101583839918718_9eb9cd58b9ea5e04c890326b5c1f471f.png#align=left&display=inline&height=408&margin=%5Bobject%20Object%5D&originHeight=430&originWidth=790&status=done&style=none&width=750)
