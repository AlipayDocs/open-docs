
# 简介
**my.offComponentError** 是用于取消监听小程序自定义组件内部 JS 代码的 error 事件。

## 使用限制

- 基础库 [1.24.9](https://opendocs.alipay.com/mini/framework/lib) 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码
```javascript
const callback = (error, method, component) => {
  console.log(error, method, component);
};
// component 组件的实例属性、方法 参见：https://opendocs.alipay.com/mini/framework/component_object#%E7%BB%84%E4%BB%B6%E5%AE%9E%E4%BE%8B%E5%B1%9E%E6%80%A7
// 监听自定义组件生命周期方法和用户自定义的组件实例方法，执行抛错时都会触发 my.onComponentError 回调。
my.onComponentError(callback);
// 取消监听
my.offComponentError(callback)
```

## 入参
| **属性** | **类型** | **描述** |
| --- | --- | --- |
| 回调函数 | Function | 自定义组件内容 JS 代码运行抛出错误时的回调函数。 |

