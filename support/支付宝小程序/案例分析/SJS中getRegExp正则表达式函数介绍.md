在 SJS 自定义脚本中不支持直接 new RegExp() 构造 regexp 对象，生成 regexp 对象需要使用 [getRegExp ](https://opendocs.alipay.com/mini/framework/datatype#regexp)函数。例如：
```
getRegExp(pattern[, flags])
```

- pattern: 正则的内容。
- flags：修饰符。只能包含以下字符：
   - g: global
   - i: ignoreCase
   - m: multiline

属性 constructor：返回字符串 "RegExp"。

| **属性** | **方法** |
| --- | --- |
| constructor：返回字符串 "**RegExp**"。 | exec |
| global | test |
| ignoreCase | toString |
| lastIndex | - |
| multiline |  |
| source |  |

**注意**：除 constructor 外属性和方法的具体含义及其使用请参考 ES5 标准。<br />示例代码：
```javascript
var
 reg = getRegExp("name", "img");
 console.log("name" === reg.source);
 console.log(true === reg.global);
 console.log(true === reg.ignoreCase);
 console.log(true === reg.multiline);
```
 
