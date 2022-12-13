注册一个 `mixin`，接受一个 Object 类型的参数。

## 版本要求
基础库 [2.8.2](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 开始支持，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。可通过 `my.canIUse('mixin')` 进行判断。

## 参数
**Object object**

| **定义段** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| props | Object | 否 | 为外部传入的数据设置默认值。 |
| data | Object | 否 | 组件内部状态。 |
| observers | Object | 否 | 数据变化观测器，用于监听 data 的变化，可查看 [数据变化观测器](https://opendocs.alipay.com/mini/04y1n6)。 |
| onInit | Function | 否 | 组件生命周期函数，组件创建时触发。 |
| deriveDataFromProps | Function | 否 | 组件生命周期函数，组件创建时和更新前触发。 |
| didMount | Function | 否 | 组件生命周期函数，组件创建完毕时触发。 |
| didUpdate | Function | 否 | 组件生命周期函数，组件更新完毕时触发。 |
| didUnmount | Function | 否 | 组件生命周期函数，组件删除时触发。 |
| onError | Function | 否 | 组件方法执行抛出错误时触发。 |
| mixins | Array | 否 | 组件间代码复用机制。<br />**注意：**支持传入 `Mixin()` 的返回值，不支持传入普通的 mixin 对象。 |
| methods | Object | 否 | 组件的方法，可以是事件响应函数或任意的自定义方法。 |
| definitionFilter | Function | 否 | 定义段过滤器，用于自定义组件扩展，可查看 [自定义组件扩展](https://opendocs.alipay.com/mini/05bdpv)。 |


## 示例代码
```typescript
const mixin = Mixin({
 mixins: [Mixin({})],
  props: {
    
  },
  data: {
    
  },
  onInit() {
    
  },
  methods: {
    mixinMethod: function() {}
  }
});
```

