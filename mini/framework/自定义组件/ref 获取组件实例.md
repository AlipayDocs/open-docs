基础框架 1.18.0 起支持定义和获取自定义组件的对外实例。

# 自定义组件 ref 定义段

从基础框架 1.18.0 起，自定义组件可以在选项中配置 `ref` 方法。此方法的返回值将作为该自定义组件的对外引用实例。配置了 `ref` 后，宿主小程序和插件小程序可以互相获取对方的自定义组件对外实例。

```javascript
// components/index/index.js
Component({
  ref() {
    return {
      plus: () => this.handlePlus(),
    };
  },
  data: {
    counter: 0,
  },
  methods: {
    handlePlus() {
      this.setData({ counter: this.data.counter + 1 });
    },
  },
});
```

如果未定义 `ref` 方法，尝试引用该自定义组件的对外实例时，若是同属一个小程序宿主或插件的其他自定义组件或页面，会获得该自定义组件的 `this`；否则，获得 `null`。
# 创建后 ref 回调

如果小程序项目开启了 `component2`，就可以在 AXML 中给自定义组件定义 `ref` 回调。当被引用的自定义组件创建后，将自动触发该回调。对于未开启 `component2` 的场景，请使用 [`my.canIUse('component2')`](https://opendocs.alipay.com/mini/api/can-i-use) 做兼容。

```javascript
// /pages/index/index.js
Page({
  handlePlus() {
    this.counterRef.plus();
  },
  // 参数 ref 为自定义组件实例的对外引用
  handleRef(ref) {
    // 存储自定义组件实例，方便以后调用
    this.counterRef = ref;
  },
});
```

```html
<!-- /pages/index/index.axml -->
<my-component ref="handleRef" />
<button onTap="handlePlus">+</button>
```
# 自定义组件选择方法

自定义组件可以通过 [this.selectOwnerComponent](https://opendocs.alipay.com/mini/framework/component_object#%E7%BB%84%E4%BB%B6%E5%AE%9E%E4%BE%8B%E6%96%B9%E6%B3%95)、[this.selectComposedParentComponent](https://opendocs.alipay.com/mini/framework/component_object#%E7%BB%84%E4%BB%B6%E5%AE%9E%E4%BE%8B%E6%96%B9%E6%B3%95) 等方法获取其创建者自定义组件、事件路径父自定义组件时，返回相关父组件的实例结果与 `ref` 回调相同。

假设某页面结构如下：

```html
<!-- pages/index/index.axml -->
<my-a>
  <my-b />
</my-a>

<!-- my-a.axml -->
<view><slot /></view>

<!-- my-b.axml -->
<view><my-c /></view>
```

在各组件中调用各方法的结果是：

```javascript
// pages/index/index.js
Page({});

// my-a.js
Component({
  ref() {
    return {
      getMessage: () => 'i am a',
    };
  },
  didMount() {
    // 在页面的 .axml 中定义了 <my-a>
    console.log(this.selectOwnerComponent() === this.$page); // true
    // 事件路径上页面是 <my-a> 的父节点
    console.log(this.selectComposedParentComponent() === this.selectOwnerComponent()); // true
  },
});

// my-b.js
Component({
  ref() {
    return {
      getMessage: () => 'i am b',
    };
  },
  didMount() {
    // 在页面的 .axml 中定义了 <my-b>
    console.log(this.selectOwnerComponent() === this.$page); // true
    // <my-b> 作为默认插槽被 <my-a> 使用
    // 事件路径上 <my-a> 是 <my-b> 的父节点
    console.log(this.selectComposedParentComponent().getMessage()); // "i am a"
  },
});

// my-c.js
Component({
  didMount() {
    // 在 my-b.axml 中定义了 <my-c>
    console.log(this.selectOwnerComponent().getMessage()); // "i am b"
    // 事件路径上 <my-b> 是 <my-c> 的父节点
    console.log(this.selectComposedParentComponent() === this.selectOwnerComponent()); // true
  },
});
```
