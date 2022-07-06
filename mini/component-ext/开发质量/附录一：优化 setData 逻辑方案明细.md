
# 优化 setData 逻辑
任何页面变化都会触发 setData，同一时间可能会有多个 setData 触发页面进行重新渲染。如下四个接口都会触发 web-view 页面重新渲染。

- Page.prototype.setData：触发整个页面做差异比较；
- Page.prototype.$spliceData：针对长列表做优化，避免每次传递整个列表，触发整个页面做差异比较；
- Component.prototype.setData：只会从对应组件节点开始做差异比较；
- Component.prototype.$spliceData：针对长列表做优化，避免每次传递整个列表，只会从对应组件节点开始做差异比较。

# 优化建议

- 避免频繁触发 setData 或者 $spliceData，不管是页面级别还是组件级别。在我们分析的案例中，有些页面有倒计时逻辑，但是有的倒计时过于频繁触发（ms 级别的触发）；
- 需要频繁触发重新渲染时，避免使用页面级别的 setData 和 $spliceData， 将这一块封装成自定义组件，然后使用组件级别的 setData 或 $spliceData 触发组件重新渲染；
- 长列表数据触发渲染时，使用 $spliceData 多次追加数据，而不用传递整个列表；
- 复杂页面建议封装成自定义组件，减少页面级别的 setData。

# 优化案例
推荐指定路径设置数据
```java
this.setData({
  'array[0]': 1,
  'obj.x':2,
});
```
不推荐如下用法（虽然拷贝了 this.data，仍然直接更改了其属性）
```java
const array = this.data.array.concat();
array[0] = 1;
const obj={...this.data.obj};
obj.x=2;
this.setData({array,obj});
```
更不推荐直接更改 this.data（违反不可变数据原则）
```java
this.data.array[0]=1;
this.data.obj.x=2;
this.setData(this.data)
```
长列表使用 $spliceData
```java
this.$spliceData({ 'a.b': [1, 0, 5, 6] })
```

## 注意
有时业务逻辑封装到了组件中，当组件 UI 需要重新渲染时，只需在组件内部调用 setData。但有时需要从页面触发组件重新渲染，比如在页面上监听了 onPageScroll 事件，当事件触发时，需要通知对应组件重新渲染，此时的处理措施如下所示：
```javascript
// pages/index/index.js
Page({
    onPageScroll(e) {
        if (this.xxcomponent) {
            this.xxcomponent.setData({
                scrollTop: e.scrollTop            })
        }
    }
})
```
```javascript
// components/index/index.js
Component({
    didMount(){
        this.$page.xxcomponent = this;
    }
})
```
可在组件的 didMount 中将组件挂载到对应的页面上，即可在页面中调用组件级别的 setData 只触发组件重新渲染。

# 相关文档
[性能解决方案](https://opendocs.alipay.com/mini/018tp6)
