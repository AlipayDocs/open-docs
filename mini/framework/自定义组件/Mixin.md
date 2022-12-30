注册一个 `mixin`，接受一个 Object 类型的参数。

## 版本要求
- 基础库 [2.8.2](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 开始支持，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。可通过 `my.canIUse('mixin')` 进行判断。
- 基础库 [2.8.5](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2)  开始支持小程序页面设置 mixins 字段以引用 Mixin 实例，可通过 my.canIUse('page.mixins') 进行判断。
# 注意
Page 引用 mixin 与 Component 引用 mixin 相比，有以下区别:
- Mixin 定义段 props、onInit、deriveDataFromProps、didMount、didUpdate、didUnmount、onError、lifetimes、relations 会被忽略。
- pageEvents 内的页面生命周期函数/页面事件处理函数与 page.events 得触发时机一致。
- methods 内的事件响应函数或自定义方法会被解构赋值作为 Page 实例的方法，但优先级小于 Page 构造器本身定义的方法。

## 参数
**Object object**

| **定义段** | **类型** | **必填** | **描述** | **最低版本** |
| --- | --- | --- | --- | --- |
| props | Object | 否 | 为外部传入的数据设置默认值。 <br />**注意：** 被 Page 引用时，此定义段无效。| - |
| data | Object | 否 | 组件内部状态。 |
| observers | Object | 否 | 数据变化观测器，用于监听 data 的变化，可查看 [数据变化观测器](https://opendocs.alipay.com/mini/04y1n6)。 | - |
| onInit | Function | 否 | 组件生命周期函数，组件创建时触发。<br />**注意：** 被 Page 引用时，此定义段无效。 | - |
| deriveDataFromProps | Function | 否 | 组件生命周期函数，组件创建时和更新前触发。<br />**注意：** 被 Page 引用时，此定义段无效。 | - |
| didMount | Function | 否 | 组件生命周期函数，组件创建完毕时触发。 <br />**注意：** 被 Page 引用时，此定义段无效。| - |
| didUpdate | Function | 否 | 组件生命周期函数，组件更新完毕时触发。<br />**注意：** 被 Page 引用时，此定义段无效。 | - |
| didUnmount | Function | 否 | 组件生命周期函数，组件删除时触发。 <br />**注意：** 被 Page 引用时，此定义段无效。| - |
| onError | Function | 否 | 组件方法执行抛出错误时触发。 <br />**注意：** 被 Page 引用时，此定义段无效。| - |
| mixins | Array | 否 | 组件间代码复用机制。<br />**注意：** 支持传入 `Mixin()` 的返回值，不支持传入普通的 mixin 对象。 | - |
| methods | Object | 否 | 组件的方法，可以是事件响应函数或任意的自定义方法。<br />**注意：** 被 Page 引用时，会解构赋值作为 page 实例的方法，但优先级小于 Page 构造器本身定义的方法。 | - |
| definitionFilter | Function | 否 | 定义段过滤器，用于自定义组件扩展，可查看 [自定义组件扩展](https://opendocs.alipay.com/mini/05bdpv)。 | - |
| lifetimes | Object | 否 | 树维度生命周期。<br />**注意：** 被 Page 引用时，此定义段无效。 | [2.8.5](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) |
| pageEvents | Object | 否 | 组件所在页面的页面生命周期以及页面事件处理函数声明。<br />**注意：** 被 Page 引用时，此定义段会被认为是 [events](https://opendocs.alipay.com/mini/framework/page-detail#events) 定义段。 | [2.8.5](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2)  |
| relations | Object | 否 | 组件间关系定义。可查看 [组件间关系](https://opendocs.alipay.com/mini/069w9y)。 | [2.8.5](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2)  |


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

