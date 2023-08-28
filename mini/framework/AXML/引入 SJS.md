`import-sjs` 标签用于将 SJS 脚本文件定义的符号引入当前 AXML 文件，并在表达式中使用。更多关于 SJS 的介绍可查看 [SJS 介绍](https://opendocs.alipay.com/mini/framework/sjs)。
```javascript
// util.sjs
export default {
  message: 'hello alipay',
  getMsg: x => x,
};
```
```html
<!-- page.axml -->
<import-sjs name="util" from="./util.sjs"/>
<view> 使用变量 {{util.message}}</view>
<view> 使用函数 {{util.getMessage(msg)}}</view>
```

通过 `<import-sjs />` 标签，只能使用 SJS 通过 `export` 语法导出的符号。并遵循如下规则。
## 默认导出
通过 `export default` 导出的 **默认导出** 符号，必须通过 `<import-sjs name="module"/>` 来引入。<br />`import-sjs` 功能标签的 `name` 属性必须是一个合法的标识符 `/^[A-Za-z_][A-Za-z0-9_]*$/`。


## 具名导出
通过 `export const a` 导出的 **具名** 符号，必须通过 `<import-sjs name="{ a }"/>` 来引入。<br />`import-sjs` 功能标签的 `name` 属性满足以下规则

- 是一个 `Object` 字面量表达式
- `Object` 的 `key` 和 `value` 均是一个 **标识符**

以下是一个复杂示例：
```javascript
// helper.sjs
export const a = 1;
export function b() { return 2 }
```
```html
<!-- page.axml -->
<import-sjs from="./helper.sjs"  name="{ a, b: c }"/>
<view>{{ c() }}:{{a}}:{{ b }}</view>
<!-- 等价于 -->
<view>{{ 2 }}:{{ 1 }}:{{ undefined }}</view>
```

需要注意：

- 如果 `name` 出现 **默认导出** 的同名，会在编译期直接覆盖（即不论 `<import-sjs>` 标签的顺序，被覆盖的 _默认导出_ 符号在整个 AXML 中均不可访问）。
- 如果 `name` 出现 **具名导出** 的同名，会直接抛出编译异常。
