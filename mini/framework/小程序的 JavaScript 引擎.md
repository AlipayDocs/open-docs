# 运行引擎

小程序的 JavaScript 代码分为逻辑层脚本和 SJS 脚本，它们运行在相同的 JavaScript 引擎的不同线程中。

在不同操作系统上，小程序的 JavaScript 引擎是不同的。在 iOS 平台上，脚本运行在操作系统提供的 JavaScriptCore 引擎上；而在 Android 平台上，脚本则运行在支付宝提供的 V8 引擎上。

支付宝小程序通过对开发者上传的代码进行 [Babel](https://babeljs.io/) 转换，使 JavaScript 引擎支持绝大多数 ES6 的新特性。但是，对于 ES6 扩展的内置对象，小程序并未在 JavaScript 引擎上提供 polyfill，因此在不同平台的 JavaScript 引擎中，对不同的 ES6 扩展的内置对象支持存在差异。

开发者需要避免使用 JavaScript 引擎不支持的内置对象。如果必须使用，可以自己提供内置对象的 polyfill（Polyfill：用于实现浏览器或其它 JavaScript 引擎不支持的原生 API 的代码）。

**注意**：小程序引擎中禁止访问 `globalThis`、`global`，因此无法直接使用 [Babel-polyfill](https://babeljs.io/docs/en/babel-polyfill)。

# 客户端引擎的支持情况
## 各操作系统对 ES6 扩展内置对象支持情况

下表是各操作系统对 ES6 扩展的内置对象的支持情况：

| Object | iOS 8 | iOS 9 | iOS 10 及以上 | Android |
| ------ | ----- | ----- | ------------ | ------- |
| Object.is | 不支持 | 支持 | 支持 | 支持 |
| Object.assign | 不支持 | 支持 | 支持 | 支持 |
| Object.keys | 支持 | 支持 | 支持 | 支持 |
| Object.getOwnPropertyDescriptor | 支持 | 支持 | 支持 | 支持 |
| Object.getOwnPropertyNames | 支持 | 支持 | 支持 | 支持 |
| Object.getOwnPropertySymbols | 不支持 | 支持 | 支持 | 支持 |

| String | iOS 8 | iOS 9 | iOS 10 及以上 | Android |
| ------ | ----- | ----- | ------------ | ------- |
| String.prototype.codePointAt | 不支持 | 支持 | 支持 | 支持 |
| String.prototype.normalize | 不支持 | 不支持 | 支持 | 支持 |
| String.prototype.includes | 不支持 | 支持 | 支持 | 支持 |
| String.prototype.startsWith | 不支持 | 支持 | 支持 | 支持 |
| String.prototype.endsWith | 不支持 | 支持 | 支持 | 支持 |
| String.prototype.repeat | 不支持 | 支持 | 支持 | 支持 |
| String.fromCodePoint | 不支持 | 支持 | 支持 | 支持 |

| Array | iOS 8 | iOS 9 | iOS 10 及以上 | Android |
| ----- | ------ | ----- | ------------- | ------- |
| Array.prototype.copyWithin | 不支持 | 支持 | 支持 | 支持 |
| Array.prototype.find | 支持 | 支持 | 支持 | 支持 |
| Array.prototype.findIndex | 支持 | 支持 | 支持 | 支持 |
| Array.prototype.fill | 支持 | 支持 | 支持 | 支持 |
| Array.prototype.entries | 支持 | 支持 | 支持 | 支持 |
| Array.prototype.keys | 支持 | 支持 | 支持 | 支持 |
| Array.prototype.values | 不支持 | 支持 | 支持 | 不支持 |
| Array.prototype.includes | 不支持 | 支持 | 支持 | 支持 |
| Array.from | 不支持 | 支持 | 支持 | 支持 |
| Array.of | 不支持 | 支持 | 支持 | 支持 |

| Number | iOS 8 | iOS 9 | iOS 10 及以上 | Android |
| ------ | ------ | ----- | ------------- | ------- |
| Number.isFinite | 不支持 | 支持 | 支持 | 支持 |
| Number.isNaN | 不支持 | 支持 | 支持 | 支持 |
| Number.parseInt | 不支持 | 支持 | 支持 | 支持 |
| Number.parseFloat | 不支持 | 支持 | 支持 | 支持 |
| Number.isInteger | 不支持 | 支持 | 支持 | 支持 |
| Number.EPSILON | 不支持 | 支持 | 支持 | 支持 |
| Number.isSafeInteger | 不支持 | 支持 | 支持 | 支持 |

| Math | iOS 8 | iOS 9 | iOS 10 及以上 | Android |
| ---- | ------ | ----- | ------------- | ------- |
| Math.trunc | 支持 | 支持 | 支持 | 支持 |
| Math.sign | 不支持 | 支持 | 支持 | 支持 |
| Math.cbrt | 支持 | 支持 | 支持 | 支持 |
| Math.clz32 | 支持 | 支持 | 支持 | 支持 |
| Math.imul | 支持 | 支持 | 支持 | 支持 |
| Math.fround | 支持 | 支持 | 支持 | 支持 |
| Math.hypot | 支持 | 支持 | 支持 | 支持 |
| Math.expm1 | 支持 | 支持 | 支持 | 支持 |
| Math.log1p | 支持 | 支持 | 支持 | 支持 |
| Math.log10 | 支持 | 支持 | 支持 | 支持 |
| Math.log2 | 支持 | 支持 | 支持 | 支持 |
| Math.sinh | 支持 | 支持 | 支持 | 支持 |
| Math.cosh | 支持 | 支持 | 支持 | 支持 |
| Math.tanh | 支持 | 支持 | 支持 | 支持 |
| Math.asinh | 支持 | 支持 | 支持 | 支持 |
| Math.acosh | 支持 | 支持 | 支持 | 支持 |
| Math.atanh | 支持 | 支持 | 支持 | 支持 |

| 内置对象 | iOS 8   | iOS 9   | iOS 10 及以上| Android |
| ---------- | -------- | ------- | -------------- | ------- |
| Set        | 支持     | 支持    | 支持          | 支持   |
| Map        | 支持     | 支持    | 支持          | 支持   |
| WeakMap    | 支持     | 支持    | 支持          | 支持   |
| WeakSet    | 不支持   | 支持    | 支持          | 支持   |
| Symbol     | 不支持   | 支持    | 支持          | 支持   |
| Proxy      | 不支持   | 不支持  | 支持          | 支持   |
| Reflect    | 不支持   | 不支持  | 支持          | 支持   |
| Promise    | 支持     | 支持    | 支持          | 支持   |
## 各操作系统对 Date 的支持情况

通过 `new Date(...)` 解析日期字符串时，iOS 系统不支持使用短线连接的日期形式，即：

| 执行代码                                        | iOS   | Android |
| ----------------------------------------------- | ----- | ------- |
| `new Date("yyyy-MM-dd HH:mm:ss").getTime()` | 不支持 | 支持    |
| `new Date("yyyy/MM/dd HH:mm:ss").getTime()` | 支持  | 支持    |


# 对动态执行脚本的限制

出于安全考虑，小程序限制了部分 ES 的语法和 API：

- 不支持 `eval` 使用。
- `setTimeout` 和 `setInterval` 函数仅支持函数做回调参数，不可动态执行代码。
- 不支持使用 `new Function` 创建函数。


# 模块名保留字

小程序的逻辑层支持 ES2015 模块化语法，但是将浏览器部分内置对象名（如 `window`、`document`）作保留字使用，以应对未来的不时之需，这些保留字不可用做模块名。保留字有：`globalThis`、`global`、`AlipayJSBridge`、`fetch`、`self`、`window`、`document`、`location`、`XMLHttpRequest`。更多详情可查看 [框架概述](https://opendocs.alipay.com/mini/framework/overview) 中对模块名保留字的介绍。


# 相关文档

- [框架概述](https://opendocs.alipay.com/mini/framework/overview)
- [babel](https://babeljs.io/)
- [babel-polyfill](https://babeljs.io/docs/en/babel-polyfill)
