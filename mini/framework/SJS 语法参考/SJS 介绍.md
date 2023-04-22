SJS（Safe/Subset JavaScript）是小程序定义的一套脚本语言，由它导出的变量/函数可以 [在 `AXML` 中使用](https://opendocs.alipay.com/mini/framework/import-sjs)。

## 语言概述

**语法定义**  
SJS 是 JavaScript 语言的子集，并不等同于 JavaScript。具体可参考：  
- [变量](https://opendocs.alipay.com/mini/framework/sjs-variable)
- [数据类型](https://opendocs.alipay.com/mini/framework/datatype)
- [运算符](https://opendocs.alipay.com/mini/framework/operator)
- [语句](https://opendocs.alipay.com/mini/framework/sjs-statement)
- [基础类库](https://opendocs.alipay.com/mini/framework/basic-library)

**模块管理**  
- SJS 文件的扩展名必须为 `.sjs`，每个 .sjs 文件为一个模块，使用 export 导出变量和函数，使用 import 引入依赖的其他 SJS 模块。
- SJS 也可引用 npm 包，但只能引用其中的 .sjs 文件。

**运行环境**  
- SJS 运行在小程序渲染层，与小程序的 JavaScript 运行环境（逻辑层）隔离，因而不能调用 JS 文件中定义的函数，也不能调用小程序提供的 API。
- SJS 中定义的函数可用于响应基础组件的事件以避免逻辑层和渲染层的频繁通信，但有一定的限制，详见 [SJS 响应事件](https://opendocs.alipay.com/mini/01og7z)。


## 使用示例

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

```javascript
// pages/index/bar.sjs

import { five } from './foo.sjs';
export const x = 3;
export const y = 4 + five;
```

```javascript
// pages/index/index.js

Page({
  data: {
    message: 'hello javascript',
    value: 3.14159,
  },
});
```

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

**页面渲染结果：**  
```text
js message: hello javascript
sjs message: hello sjs
formatted value: 3.14
x: 3
z: 9
```
