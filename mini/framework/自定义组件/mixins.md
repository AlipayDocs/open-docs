## 概述

开发者有时可能会实现多个自定义组件，而这些自定义组件可能会有些公共逻辑要处理。小程序提供 mixins，用于解决这种情况。

示例代码：

```javascript
// /mixins/lifecycle.js
export default {
  onInit() {
    console.log('init');
  },
  deriveDataFromProps(nextProps) {},
  didMount() {},
  didUpdate(prevProps, prevData) {},
  didUnmount() {},
};
```

**注意**：`onInit` 与 `deriveDataFromProps` 自基础库 `1.14.0` 开始支持。可以使用 `my.canIUse('component2')` 做兼容判断。并且，使用 component2 的相关功能，需要在 IDE 中的 **详情** > **项目配置** 中，勾选 component2。

```javascript
// /components/index/index.js
import lifecycle from '/mixins/lifecycle';
const initialState = {
  data: {
    isLogin: false,
  },
};
const defaultProps = {
  props: {
    age: 30,
  },
};
const methods = {
  methods: {
    onTapHandler() {},
  },
};
Component({
  mixins: [lifecycle, initialState, defaultProps, methods],
  data: {
    name: 'Alipay',
  },
});
```

```html
<!-- /components/index/index.axml -->
<view>{{name}}：{{age}}</view>
```
## Mixin

基础库 [2.8.2](https://opendocs.alipay.com/mini/framework/lib) 版本起，自定义组件的参数 mixins 支持通过 `Mixin()` 注册生成的 mixin。与直接传入普通 JS 对象相比，通过 Mixin 注册生成的 mixin 有以下三个差异：

- Mixin 支持 [mixins](https://opendocs.alipay.com/mini/framework/component_object#%E5%8F%82%E6%95%B0%E8%AF%B4%E6%98%8E) 参数，即能嵌套传入 mixin。
- Mixin 注册的 mixin 实例支持自定义组件扩展机制。
- 可通过自定义组件实例方法 `hasMixin` 判断当前自定义组件是否引入了特定的 Mixin 实例。

## 同名字段的覆盖和组合规则

组件和它引用的 mixin 可以包含同名的字段，这些字段的处理方法如下：

- 如果存在同名的属性（props）或方法（methods）：
   1. 如果组件有这个属性或方法，则组件的属性会覆盖 mixin 中的同名属性或方法。
   2. 如果组件本身没有这个属性或方法，则组件的 [mixins](https://opendocs.alipay.com/mini/framework/component_object#%E5%8F%82%E6%95%B0%E8%AF%B4%E6%98%8E) 参数中定义靠后的 mixin 的属性或方法会覆盖靠前的同名属性或方法。
   3. 在上述基础上，若存在嵌套引用 mixin 的情况（只有 Mixin 支持嵌套引用，且被引用的 mixin 必须是 Mixin 实例），则规则为：引用者 mixin 的同名属性或方法会覆盖被引用的 mixin 实例中的同名属性或方法。
- 如果存在同名的内部数据字段（data）：
   1. 如果组件已定义这个数据字段，则组件的数据字段会覆盖 mixin 中的同名数据字段。
   2. 如果组件没有这个数据字段，则：引用者 mixin 优先于被引用的 mixin（只有 Mixin 支持嵌套引用，且被引用的 mixin 必须是 Mixin 实例），靠后的 mixin 会覆盖靠前的同名字段（优先级高者覆盖优先级低者）。
- 生命周期函数和 observers 不相互覆盖，而是在各自的触发时机被依次调用：
   - 不同生命周期函数间遵循组件生命周期函数的执行顺序。
   - 相同生命周期函数和同字段 observers 遵循如下规则：
      - mixin 优先于组件执行。
      - 被引用的 mixin 优先于引用者 mixin 执行（只有 Mixin 支持嵌套引用，且被引用的 mixin 必须是 Mixin 实例）。
      - 靠前的 mixin 优先于靠后的 mixin 执行；
   - 如果同一个 mixin（需是 Mixin 实例）被一个组件多次引用，它定义的生命周期函数和 observers 会执行多次。

# 相关文档

- [component2 Demo](https://github.com/ant-mini-program/component2-demo)
- [my.canIUse](https://opendocs.alipay.com/mini/api/can-i-use)
