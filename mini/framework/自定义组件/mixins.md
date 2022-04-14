开发者有时可能会实现多个自定义组件，而这些自定义组件可能会有些公共逻辑要处理，小程序提供 mixins 用于解决这种情况。

示例代码：
```javascript
// /mixins/lifecycle.js
export default {
  onInit(){
    console.log('init');
  }, 
  deriveDataFromProps(nextProps){},
  didMount(){},
  didUpdate(prevProps,prevData){},
  didUnmount(){},
};
```
**注意**: `onInit` 与 `deriveDataFromProps` 自基础库 `1.14.0` 开始支持，可以使用 `my.canIUse('component2')` 做兼容判断，并且，使用 component2 的相关功能，需要在 IDE 中的 **详情** > **项目配置** 中，勾选 component2。
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
}
Component({
  mixins: [
    lifecycle,
    initialState,
    defaultProps,
    methods
  ],
  data: {
    name: 'alipay',
  },
});
```
```html
<!-- /components/index/index.axml -->
<view>{{name}}: {{age}}</view>
```

# 相关文档
- [component2 Demo](https://github.com/ant-mini-program/component2-demo)
- [my.canIUse](https://opendocs.alipay.com/mini/api/can-i-use)

