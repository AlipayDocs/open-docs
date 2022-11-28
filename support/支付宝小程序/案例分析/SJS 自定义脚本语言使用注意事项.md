## SJS 使用注意事项
- SJS 中只支持使用 import、export 管理模块依赖。
- SJS 只能定义在 .sjs 文件中。然后在 axml 中使用 <import-sjs> 标签引入。
- SJS 可以调用其它 sjs 文件中定义的函数。
- SJS 是 JavaScript 语言的子集，与 JavaScript 是不同的语言，其语法并不与 JavaScript 一致，请勿将其等同于 JavaScript。
- SJS 的运行环境和其它 JavaScript 代码是隔离的， sjs 中不能调用其它 JavaScript 文件中定义的函数，也不能调用小程序提供的 API。
- SJS 函数不能作为组件事件回调。
- SJS 不依赖于基础库版本，可以在所有版本小程序中运行。

## import-sjs 标签引用注意事项

- 在单个 AXML 文件内，建议将 name 值设为唯一。
- 若有重复模块名则按照先后顺序覆盖（后者覆盖前者）。
- 不同 AXML 文件之间的 <import-sjs> 模块名不会相互覆盖。
- name 属性可使用一个字符串表示默认模块名，也可使用 {x} 表示命名模块的导出。
- 引用时务必使用 `.sjs` 文件后缀。
- 若定义了一个 .sjs 模块，但从未引用，则该模块不会被解析与运行。

## 相关文档

- [SJS 介绍](https://opendocs.alipay.com/mini/framework/sjs)
- [运算符](https://opendocs.alipay.com/mini/framework/operator)
- [语句](https://opendocs.alipay.com/mini/framework/sjs-statement)
- [变量](https://opendocs.alipay.com/mini/framework/sjs-variable)
