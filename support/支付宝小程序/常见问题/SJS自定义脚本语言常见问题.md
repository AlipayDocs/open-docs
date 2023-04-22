## 说明

- **sjs 中只支持使用 import、export 管理模块依赖。**
- sjs 只能定义在 .sjs 文件中。然后在 axml 中使用 <import-sjs> 标签引入。
- sjs 可以调用其它 sjs 文件中定义的函数。
- sjs 是 JavaScript 语言的子集，请勿将其等同于 JavaScript。
- sjs 的运行环境和其它 JavaScript 代码是隔离的， sjs 中不能调用其它 JavaScript 文件中定义的函数，也不能调用小程序提供的 API。
- sjs 函数不能作为组件事件回调。
- sjs 不依赖于基础库版本，可以在所有版本小程序中运行。
- 引用时务必使用 “.sjs” 文件后缀。
- 若定义了一个 .sjs 模块，但从未引用，则该模块不会被解析与运行。
- 在单个 AXML 文件内，建议将<import-sjs> 的属性 name 值设为唯一。若有重复模块名则按照先后顺序覆盖（后者覆盖前者）。
- 不同 AXML 文件之间的 <import-sjs> 模块名不会相互覆盖。name 属性可使用一个字符串表示默认模块名，也可使用 {x} 表示命名模块的导出。** **

## 常见问题

### SJS变量语法和变量名命名规则
参考[SJS变量语法和变量名命名规则](https://opendocs.alipay.com/support/01rb0n)。 

### sjs自定义脚本语言使用注意事项
参考[sjs自定义脚本语言使用注意事项](https://opendocs.alipay.com/support/01rb0o)。 

### 小程序js如何使用正则表达式
参考[小程序js如何使用正则表达式](https://opendocs.alipay.com/support/01rb7a)。 

### SJS中getRegExp正则表达式函数介绍
参考[SJS中getRegExp正则表达式函数介绍](https://opendocs.alipay.com/support/01rb1p)。 

### js中引入sjs报：getRegExp is not defined
参考[js中引入sjs报：getRegExp is not defined](https://opendocs.alipay.com/support/01rb39)。 

### Cannot read property 'setData' of undefined
参考[Cannot read property 'setData' of undefined](https://opendocs.alipay.com/support/01rb61)。 

### 有没有类似vue的nextTick方法
支付宝小程序目前没有类似 Vue 的 nextTick 方法。子组件在父组件 onLoad 事件执行完成之后，子组件才开始执行的方法。 

### JS中报错无法读取空的属性原因

- 排查该对象在 toString 时是否为空。可对toString方法进行非空判断。
- 加载 JS 的时候页面还未加载完成导致对象为空。可将 JS 放在页面下部要让页面加载完成后再加载这段 JS 代码。 

### can not find event handle method
原因：没有在页面 JS中找到 axml 中事件定义的方法。<br />解决：检查 axml 指的的事件名称与js中的方法名是否一致。<br /> 
