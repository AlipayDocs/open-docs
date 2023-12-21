SJS (Safe/Subset JavaScript) 是专为小程序设计的脚本语言。作为 JavaScript 的子集，它支持 JavaScript 的部分功能，但不是全部。它的主要特点是变量和函数可以直接在小程序的 AXML 中使用，提高了开发效率和安全性。

## 详细特性

### 语法规则与特性

SJS 遵从 JavaScript 的基本语法，但作为子集，并非支持 JavaScript 的所有特性。详细信息可参考以下链接：

- [变量](https://opendocs.alipay.com/mini/framework/sjs-variable)
- [数据类型](https://opendocs.alipay.com/mini/framework/datatype)
- [运算符](https://opendocs.alipay.com/mini/framework/operator)
- [语句](https://opendocs.alipay.com/mini/framework/sjs-statement)
- [基础类库](https://opendocs.alipay.com/mini/framework/basic-library)

### 模块化特性

- **文件格式**：`.sjs` 文件，每个文件是一个模块。
- **导入导出**：使用 `export` 导出变量和函数，通过 `import` 引入其他 SJS 模块。
- **对 npm 支持**：SJS 支持引用 npm 包中的 `.sjs` 文件。

### 运行环境

SJS 在小程序的渲染层中运行，与逻辑层的 JavaScript 环境隔离。具体来说：

- SJS 不能调用 JS 文件中定义的函数或小程序提供的 API。
- SJS 可用于处理基础组件的事件响应，减少逻辑层和渲染层间的通信。
- 使用 SJS 有一定限制，详见：[SJS 响应事件](https://opendocs.alipay.com/mini/01og7z)。

## 使用示例

以下是 SJS 的基本使用示例，展示了如何定义和使用 SJS 脚本。

### 定义 SJS 模块

```javascript
// pages/index/foo.sjs
const message = 'hello sjs';
const format = num => num.toFixed(2);
const five = 5;
export default {
  message,
  format,
  five
};
```

### 引入和使用其他 SJS 模块

```javascript
// pages/index/bar.sjs
import { five } from './foo.sjs';
export const x = 3;
export const y = 4 + five;
```

### 小程序页面的 JavaScript 部分

```javascript
// pages/index/index.js
Page({
  data: {
    message: 'hello javascript',
    value: 3.14159,
  },
});
```

### 小程序页面的 AXML 部分

```html
<!-- pages/index/index.axml -->
<import-sjs from="./foo.sjs" name="m" />
<import-sjs from="./bar.sjs" name="{x, y: z}" />
<view>js message: {{message}}</view>
<view>sjs message: {{m.message}}</view>
<view>formatted value: {{m.format(value)}}</view>
<view>x: {{x}}</view>
<view>z: {{z}}</view>
```

### 页面渲染结果

```text
js message: hello javascript
sjs message: hello sjs
formatted value: 3.14
x: 3
z: 9
```
