从 `1.14.0` 版本开始，自定义组件支持使用 ref 获取自定义组件实例，可以使用 [my.canIUse('component2') ](https://opendocs.alipay.com/mini/api/can-i-use)做兼容。 并且，需要在 IDE 中的 **详情** > **项目配置** 中，勾选 component2。
```javascript
// /pages/index/index.js
Page({
  plus() {
    this.counter.plus();
  },
  // saveRef 方法的参数 ref 为自定义组件实例，运行时由框架传递给 saveRef
  saveRef(ref) {
	// 存储自定义组件实例，方便以后调用
    this.counter = ref;
  },
});
```
```html
<!-- /pages/index/index.axml -->
<my-component ref="saveRef" />
<button onTap="plus">+</button>
```
**说明**：

- 使用`ref` 绑定 `saveRef` 之后，会在组件初始化时触发 `saveRef` 方法。
- `saveRef`方法的参数`ref`为自定义组件实例，由框架传递给`saveRef`方法。
- `ref` 同样可以用于父组件获取子组件的实例。

```javascript
// /components/index/index.js
Component({
  data: {
    counter: 0,
  },
  methods: {
    plus() {
      this.setData({ counter: this.data.counter + 1 })
    },
  },
})
```
```html
<!-- /components/index/index.axml -->
<view>{{counter}}</view>
```

## 自定义组件 ref 定义段
自基础库 `1.18.0` 开始，自定义组件（component2）支持使用 ref 定义段指定调用者传递ref时获取的值。 未使用 ref 定义段时，调用者传递ref获取的值是自定义组件的 `this` （插件的自定义组件将返回 `null`)。 使用这个定义段时，将以这个定义段的函数返回值代替。
```javascript
// 自定义组件内部
// /components/index/index.js
Component({
  ref() {
    return { key: 'value' }
  }
```
```html
<!-- 使用自定义组件时 -->
<!-- /pages/index/index.axml -->
<my-component ref="saveRef" />
```
```javascript
// /pages/index/index.js
Page({
  // 此时saveRef 方法的参数 ref 即是 my-component 自定义组件中的 ref 定义段的返回值
  saveRef(ref) {
	// 存储自定义组件实例，方便以后调用
    this.counter = ref; // 等于 { key: 'value' }
  },
});
```

## 相关文档

- [自定义组件介绍](https://opendocs.alipay.com/mini/framework/custom-component-overview)
- [my.canIUse](https://opendocs.alipay.com/mini/api/can-i-use)

