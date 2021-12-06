
# 简介
用以提供常见类型的业务异常展示视图。

## 使用场景

- 界面的视图界面依赖网络接口返回数据，当业务服务器 **触发限流或发生异常** 时，可展示 **统一异常页** ，避免白屏等现象，提升用户体验。
- 业务预期内的异常状态，如该用户无订单记录，无社保记录等**空状态**。
- 业务非预期内的一些逻辑执行失败，可跳转到统一异常页。

## 使用限制
版本要求基础库 [2.7.0](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 及以上，若版本较低，建议做 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。

# 使用

## 示例代码

### 定制文案
可以通过 `title` 字段和 `message` 定制默认文案。
```html
<!-- 全屏异常视图 -->
<error-view
   fullscreen
   type="default"
   title="主要文案"
   message="次要文案"
>
</error-view>
```

### 定制按钮行为
可以通过在 error-view 内嵌入组件的方式，定制默认行为：

- 可以直接使用 [button](https://opendocs.alipay.com/mini/component/button) 组件，通过绑定 tap 自定义事件的方式，自定义操作行为。<br />
- 如果希望自主触发 返回（navigateBack） / 刷新（reload）行为，可以使用 [navigator](https://opendocs.alipay.com/mini/component/navigator) 导航组件来完成。
```html
<!-- 定制默认行为 -->
<error-view 
  type="default"
>
  <button size="mini" type="ghost" onTap="onTap1">操作1</button>  
  <navigator open-type="reload">
    <button size="mini" type="ghost">刷新文案</button>  
  </navigator>
</error-view>
```

### 自定义异常详细信息
当发生特定业务异常时，可以传递 `data-` 字段信息。
```html
<!-- 全屏异常视图 -->
<view class="page">
  <error-view
  	type="default" title="主要文案" message="次要文案"
    data-url="{{errorUrl}}"
    data-status="{{errorStatus}}"
    data-message="{{errorMessage}}"
  >
  </error-view>
</view>
```

## 属性说明
| **属性** | **类型** | **描述** |
| --- | --- | --- |
| fullscreen | Boolean | 是否展示全屏错误视图，状态图案及文案大小会有差异。 |
| type | String | 异常类型。<br />**可选值**：default、busy、error、network、trade<br />**默认值**：default |
| title | String | 异常状态主要文案，详情参见 [默认界面及文案](https://opendocs.alipay.com/mini/component/error-view#%E9%BB%98%E8%AE%A4%E7%95%8C%E9%9D%A2%E5%8F%8A%E6%96%87%E6%A1%88)。 |
| message | String | 异常状态次要文案，仅在全屏状态显示，详情参见 [全屏状态](https://opendocs.alipay.com/mini/component/error-view#%E5%85%A8%E5%B1%8F%E7%8A%B6%E6%80%81)。 |
| title-color | HexColor | 异常状态主要文案的自定义颜色。 |
| message-color | HexColor | 异常状态次要文案的自定义颜色。 |


## 默认界面及文案
针对不同的 `type` 类型，全屏状态 `fullscreen` 与非全屏状态有如下示例，在不同类型下，提供了 **返回** 或 **刷新** 默认行为。

### 全屏状态
| **type** | **default** | **busy** | **error** | **network** | **trade** |
| --- | --- | --- | --- | --- | --- |
| 场景 | 通用状态 | 系统繁忙 | 系统错误 | 网络异常 | 交易失败 |
| 示例 | ![image](https://intranetproxy.alipay.com/skylark/lark/0/2021/png/1613/1617785668943-f7accc1b-cab5-492f-9a99-154a737f4271.png) | ![image](https://intranetproxy.alipay.com/skylark/lark/0/2021/png/1613/1617785700019-77fba383-7b30-4e63-88f5-273c428d402d.png) | ![image](https://intranetproxy.alipay.com/skylark/lark/0/2021/png/1613/1617785737190-ffd37054-8ad0-47eb-9b20-d46f058d779f.png) | ![image](https://intranetproxy.alipay.com/skylark/lark/0/2021/png/1613/1617785787780-720bdd46-4445-464b-9392-c1a5c139b564.png) | ![image](https://intranetproxy.alipay.com/skylark/lark/0/2021/png/1613/1617785811364-9ece3806-b762-41ec-af42-a2d9891fbe9c.png) |


### 非全屏状态
| **type** | **default** | **busy** | **error** | **network** | **trade** |
| --- | --- | --- | --- | --- | --- |
| 场景 | 通用状态 | 系统繁忙 | 系统错误 | 网络异常 | 交易失败 |
| 示例 | ![image](https://intranetproxy.alipay.com/skylark/lark/0/2021/png/1613/1617785982226-ae0a7a62-91a9-401c-99cb-20fecfe22f0d.png) | ![image](https://intranetproxy.alipay.com/skylark/lark/0/2021/png/1613/1617786028990-87c4ae1d-53d8-4fa0-a8d2-db6780d39209.png) | ![image](https://intranetproxy.alipay.com/skylark/lark/0/2021/png/1613/1617786048193-92fe6f06-2cd5-454a-a7d3-c188f9b262b1.png) | ![image](https://intranetproxy.alipay.com/skylark/lark/0/2021/png/1613/1617786065816-ba1361bd-fa3f-4370-aa24-f31a3ed268c7.png) | ![image](https://intranetproxy.alipay.com/skylark/lark/0/2021/png/1613/1617786082519-656419da-963f-41d8-b088-3757b308850a.png) |


### 深色背景默认界面
当前不同的 `type` 类型提供的默认图案，均适配了深色背景，效果如下。 

| **type** | **default** | **busy** | **error** | **network** | **trade** |
| --- | --- | --- | --- | --- | --- |
| 场景 | 通用状态(深色) | 系统繁忙(深色) | 系统错误(深色) | 网络异常(深色) | 交易失败(深色) |
| 示例 | ![image](https://intranetproxy.alipay.com/skylark/lark/0/2021/png/1613/1617786399101-bcfd0170-453b-4c9f-96eb-0bd721a6b29f.png) | ![image](https://intranetproxy.alipay.com/skylark/lark/0/2021/png/1613/1617786423242-6a58dfdc-fb51-49fe-b6ab-61823111c76c.png) | ![image](https://intranetproxy.alipay.com/skylark/lark/0/2021/png/1613/1617786483751-bbcc1fa5-31f8-4ace-ac34-f3512dd8bc71.png) | ![image](https://intranetproxy.alipay.com/skylark/lark/0/2021/png/1613/1617786512941-e5b8391d-b09e-418c-9b5d-f69493846cb4.png) | ![image](https://intranetproxy.alipay.com/skylark/lark/0/2021/png/1613/1617786537175-32978dee-21e2-4aef-b7c2-2893fe2bb98a.png) |


## 兼容性 
目前在基础库 [2.7.0](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 版本及以上才支持，低版本会不显示该组件，可以通过以下方式判断是否支持： 
```javascript
my.canIUse('error-view') === true;
```
