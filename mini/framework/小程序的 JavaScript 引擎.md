# 运行引擎

小程序的 JavaScript 代码分为逻辑层脚本和 SJS 脚本，它们运行在相同的 JavaScript 引擎的不同线程中。

在不同操作系统上，小程序的 JavaScript 引擎是不同的。在 iOS 平台上，脚本运行在操作系统提供的 JavaScriptCore 引擎上；而在 Android 平台上，脚本则运行在支付宝提供的 V8 引擎上。

由于引擎或版本的不同，支付宝小程序的执行环境对 ECMAScript 标准的支持存在客观差异，因此支付宝小程序为开发者提供了若干能力用于抹平引擎差异。

## 语法

默认情况下，开发者可以使用部分 ES6+ 语法 (例如 `async/await`) 编写小程序，支付宝小程序会自动转换语法，以确保小程序可以在所有执行环境中正常运行。

同时，开发者可以通过 `mini.project.json` 中的 `transpile` 配置项， 让支付宝小程序支持 ES2023 规范定义的语法。具体参考 [transpile](https://opendocs.alipay.com/mini/03dbc3#transpile) 的相关说明。


**注意**：为了提高小程序编译性能，如果没有主动配置 `transpile`，小程序不会自动为 `node_modules` 中的代码转换语法。

在[支付宝开发者工具 (IDE)](https://opendocs.alipay.com/mini/02bzsm?pathHash=98121aa5) 中开发调试支付宝小程序时，小程序在原生支持新语法的模拟器中运行，因此开发者可以通过 `mini.project.json` 中的 `skipTranspile` 配置项跳过在开发时的语法转换，减少开发时的小程序编译耗时。具体参考 [skipTranspile](https://opendocs.alipay.com/mini/03dbc3#developOptions) 的相关说明。


一般而言，在支付宝小程序项目中使用如下 `mini.project.json` 配置可以满足绝大多数开发者对于较新 ES 语法的需求。

```json
{
    "format": 2,
    "compileOptions": {
        "transpile": {}
    }
}
```


## 内置对象/方法


支付宝小程序默认不对执行环境做任何处理，因此开发者所能使用的 ES 内置对象取决于运行小程序的平台。


在[支付宝开发者工具 (IDE)](https://opendocs.alipay.com/mini/02bzsm?pathHash=98121aa5) 中开发调试支付宝小程序时，开发者可能无意中使用低版本引擎中不支持的内置对象/方法等。因此，强烈建议小程序上架前，通过真机预览等功能对小程序进行功能验证。

为了减轻开发者心智负担，[支付宝小程序基础库](https://opendocs.alipay.com/mini/framework/lib?pathHash=ef31f026) 自 2.9.21 版本开始内置 polyfill ([什么是 polyfill](https://developer.mozilla.org/zh-CN/docs/Glossary/Polyfill)), 为所有平台提供统一的 ES2023 规范支持。

开发者可以通过 `app.json` 中的 `requirePolyfill` 配置项主动开启。

```json
{
    "requirePolyfill": true
}
```

**注意**：需要前往小程序管理后台设置最低基础库版本为 2.9.21+，以免部分长尾用户无法正常使用小程序。

**注意**：部分无法被 polyfill 支持的对象或方法，例如 BigInt、Atomics 和 WeakRef，在开启配置项后仍不会被支持.


### 自定义 Polyfill

如果小程序不便修改最低基础库，或是开发者希望使用一些尚未进入 ES 规范的内置对象/方法，可以选择自行引入 polyfill，例如在前端社区已经广泛使用的 core-js 等。

默认情况下，小程序代码中禁止访问 `globalThis` 和 `global` 等全局上下文对象；这可能会破坏 core-js 的正常工作。
因此请先通过 `mini.project.json` 中的 `globalObjectMode` 配置项开启全局上下文对象，具体参考 [globalObjectMode](https://opendocs.alipay.com/mini/03dbc3#globalObjectMode) 的相关说明。


**注意**：引入自定义 polyfill 可能显著影响小程序的包体积。


## 引擎对 new Date 的支持差异

不同引擎在 `new Date` 时使用的解析算法不同，因此请确保传入的时间字符串符合规范定义，否则引擎可能解析出非预期的值。

例如，iOS 平台的引擎不支持解析形如 `"yyyy-MM-dd HH:mm:ss"` 的不规范时间字符串。

具体参考 [Date.parse()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Date/parse#%E5%BC%95%E6%93%8E%E7%9B%B8%E5%85%B3%E7%9A%84%E6%97%A5%E6%9C%9F%E6%A0%BC%E5%BC%8F) 文档。


## 对动态执行脚本的限制

出于安全考虑，小程序限制了部分能够动态执行代码的能力：

- 不支持使用 `eval`
- `setTimeout` 和 `setInterval` 函数仅支持函数做回调参数，不可动态执行代码
- 不支持使用 `new Function` 创建函数

# 保留的导入符号

小程序支持使用 ES Module 组织代码，但是将浏览器部分内置对象名（如 window、document）作保留字使用，以应对未来的不时之需，这些保留字不可用做导入符号。保留字有：globalThis、global、AlipayJSBridge、fetch、self、window、document、location、XMLHttpRequest。更多详情可查看 [框架概述](https://opendocs.alipay.com/mini/framework/overview) 中对保留的导入符号的介绍。

# 相关文档

- [框架概述](https://opendocs.alipay.com/mini/framework/overview)
