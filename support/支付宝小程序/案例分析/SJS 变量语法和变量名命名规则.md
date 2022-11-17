##  SJS 变量语法规则
- var 与 JavaScript 中表现一致，会有变量提升。
- 支持 const 与 let，与 JavaScript 表现一致。
- 没有声明的变量直接赋值使用，会被定义为全局变量。
- 只声明变量而不赋值，默认值为 undefined。

### 示例代码
```js
var num = 1;
var str = "hello alipay";
var undef; // undef === undefined
const n = 2; //支持const
let s = 'string'; //支持let
globalVar = 3; //变量提升为全局变量
```

## SJS变量名命名规则
变量命名必须符合下面两个规则：

- 首字符必须是：字母（a-z,A-Z），下划线（_）。
- 首字母以外的字符可以是：字母（a-z,A-Z），下划线（_），数字（0-9）。

 
