小程序 JS 中可以使用以下两种方法之一构建一个正则表达式：

- 使用一个正则表达式字面量，其由包含在斜杠之间的模式组成，如下所示：
```
//校验手机号正则表达式
var patt=/^1d{10}$/;
//匹配结果打印，返回的是
falseconsole.log(patt.test('167534'));
```

- 或者调用 RegExp 对象的构造函数，如下所示：
```
var 
re = new RegExp("ab+c");
```
具体使用可以搜索引擎搜索相关 JavaScript 资料。

**注意：**在 SJS 自定义脚本中不支持直接 new RegExp() 构造 regexp 对象，生成 regexp 对象需要使用 [getRegExp](https://opendocs.alipay.com/support/01rb1p) 函数。<br />示例代码：
```
var 
reg = getRegExp("name", "img");
console.log("name" === reg.source);
console.log(true === reg.global);
console.log(true === reg.ignoreCase);
console.log(true === reg.multiline);
```
 
