# 简介
监听小程序异步组件（[懒加载插件](https://opendocs.alipay.com/mini/plugin/plugin-usage#%E6%87%92%E5%8A%A0%E8%BD%BD%E6%A8%A1%E5%BC%8F)、[分包异步化](https://opendocs.alipay.com/mini/057ht3)）加载失败事件。

## 使用限制

- 基础库 [2.8.1](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 或更高版本。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码
```javascript
my.onLazyLoadError((res) => {
  const { type, subpackage, plugin, errMsg } = res;
  // ...
}, 3000);
```

## 入参

### Function callback
异步组件加载失败的回调函数。必选。<br />触发时，callback 将收到一个 Object  类型的参数，属性如下。

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| type | String | <br />- subpackage：分包异步化场景。<br />- plugin：懒加载插件场景。|
| subpackage | Array | 分包异步组件所属的分包。<br />`type == 'subpackage'`  可用。 |
| plugin | Array | 懒加载插件组件所属的插件。<br />`type == '``plugin``'`  可用。 |
| errMsg | String | 详细信息。 |


### Number timeout
超时等待时间（单位：ms）。可选，默认值 5000。该设置全局有效，多次指定超时时间则覆盖前面的设置。<br />
加载异步组件通常需要下载分包，分包下载超过 timeout 值会触发 errMsg 为 `loadSubpackage: timeout` 的回调。分包确认下载失败时，会再次触发 errMsg 为 `loadSubpackage: fail` 的回调。

## 注意
若在页面中使用该接口进行监听，请确保在必要时手动调用 my.offLazyLoadError 取消监听，避免内存泄漏。
