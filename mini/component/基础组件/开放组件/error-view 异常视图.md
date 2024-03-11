# 简介

用以提供常见类型的业务异常展示视图。

## 使用场景

- 界面视图依赖网络接口返回的数据。当业务服务器触发限流或出现异常时，可展示统一异常页，避免白屏等不良体验，提升用户体验。
- 业务预期内的异常状态，例如用户没有订单记录、无社保记录等空状态。
- 对于业务非预期内一些逻辑执行失败的情况，可跳转统一异常页。

## 使用限制

- 版本要求：基础库 `2.7.0` 以上。若版本较低，建议进行[兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- Native 渲染引擎：暂不支持。是否支持可通过 `my.canIUse('error-view')` 判断。

# 使用
## 示例代码

### 定制文案

可以通过 `title` 字段和 `message` 定制默认文案。

```html
<!-- 全屏异常视图 -->
<error-view fullscreen type="default" title="主要文案" message="次要文案">
</error-view>
```

### 定制按钮行为

通过在 `error-view` 内嵌入组件的方式，可以定制默认行为：

- 直接使用 [button](https://opendocs.alipay.com/mini/component/button) 组件，通过绑定 `tap` 事件，自定义操作行为。
- 若希望主动触发“返回（navigateBack）”或“刷新（reload）”行为，可利用 [navigator](https://opendocs.alipay.com/mini/component/navigator) 导航组件实现。

```html
<!-- 定制默认行为 -->
<error-view type="default">
  <button size="mini" type="ghost" onTap="onTap1">操作1</button>
  <navigator open-type="reload">
    <button size="mini" type="ghost">刷新文案</button>
  </navigator>
</error-view>
```

### 自定义异常详细信息

当发生特定业务异常时，可通过传递 `data-` 开头的字段信息，比如 `data-url`、`data-status` 和 `data-message`。

```html
<!-- 全屏异常视图 -->
<view class="page">
  <error-view
    type="default"
    title="主要文案"
    message="次要文案"
    data-url="{{errorUrl}}"
    data-status="{{errorStatus}}"
    data-message="{{errorMessage}}"
  >
  </error-view>
</view>
```
## 属性说明

| 属性       | 类型    | 描述 |
| ---------- | ------- | ---- |
| fullscreen | Boolean | 是否展示全屏错误视图，状态图案及文案大小会有差异。 |
| type       | String  | 异常类型。可选值：`default`、`busy`、`error`、`network`、`trade`；默认值：`default`。 |
| title      | String  | 异常状态主要文案，详情可查看[默认界面及文案](https://opendocs.alipay.com/mini/component/error-view#默认界面及文案)。 |
| message    | String  | 异常状态次要文案，仅在全屏状态显示，详情可查看[全屏状态](https://opendocs.alipay.com/mini/component/error-view#全屏状态)。 |
| title-color | HexColor | 异常状态主要文案的自定义颜色。 |
| message-color | HexColor | 异常状态次要文案的自定义颜色。 |

## 默认界面及文案

根据不同的 `type` 类型，在全屏状态 `fullscreen` 与非全屏状态下有以下默认界面和文案示例。不同类型提供了“返回”或“刷新”的默认操作。

### 全屏状态

| type     | default                                                         | busy                                                          | error                                                         | network                                                       | trade                                                         |
| -------- | --------------------------------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 场景     | 通用状态                                                       | 系统繁忙                                                     | 系统错误                                                     | 网络异常                                                     | 交易失败                                                     |
| 示例     | ![image](https://cdn.nlark.com/yuque/0/2022/png/179989/1649386910497-ef355785-2e3f-4ac4-8089-326944a41555.png) | ![image](https://cdn.nlark.com/yuque/0/2022/png/179989/1649386911049-25341d0f-cb7a-4aec-82cc-9b73b7a94813.png) | ![image](https://cdn.nlark.com/yuque/0/2022/png/179989/1649386911539-1bf7b2b6-26b1-4267-8225-4a8dfcef8fc5.png) | ![image](https://cdn.nlark.com/yuque/0/2022/png/179989/1649386911978-bbe8a7f2-a1af-4f1e-9298-4cea4c60a458.png) | ![image](https://cdn.nlark.com/yuque/0/2022/png/179989/1649386912464-b1c5dc20-fe14-45a7-960e-792a346151b4.png) |

### 非全屏状态

| type     | default                                                         | busy                                                          | error                                                         | network                                                       | trade                                                         |
| -------- | --------------------------------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 场景     | 通用状态                                                       | 系统繁忙                                                     | 系统错误                                                     | 网络异常                                                     | 交易失败                                                     |
| 示例     | ![image](https://cdn.nlark.com/yuque/0/2022/png/179989/1649387036694-b79dbd75-67c9-4844-9ebe-319efbb4bb2e.png) | ![image](https://cdn.nlark.com/yuque/0/2022/png/179989/1649387041165-b1c4d22d-1e1e-4a69-84f0-992d11a538b4.png) | ![image](https://cdn.nlark.com/yuque/0/2022/png/179989/1649387045046-56ede4d7-a8fc-41d8-98d4-ea2ade1ab908.png) | ![image](https://cdn.nlark.com/yuque/0/2022/png/179989/1649387048140-3ed079d3-66fb-49a5-9d33-a3237aa686e0.png) | ![image](https://cdn.nlark.com/yuque/0/2022/png/179989/1649387051164-18e26124-8d63-4ce3-bc6c-cc0bb8a0c8cf.png) |

### 深色背景默认界面

对于不同的 `type` 类型，提供的默认图案均已适配深色背景。

| type     | default                                                         | busy                                                          | error                                                         | network                                                       | trade                                                         |
| -------- | --------------------------------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 场景     | 通用状态（深色）                                               | 系统繁忙（深色）                                             | 系统错误（深色）                                             | 网络异常（深色）                                             | 交易失败（深色）                                             |
| 示例     | ![image](https://cdn.nlark.com/yuque/0/2022/png/179989/1649387168615-3fa3202e-2ea3-4783-966c-2379de817c16.png) | ![image](https://cdn.nlark.com/yuque/0/2022/png/179989/1649387171971-24fd6d92-43b2-4fc8-80b2-c33c223d89d2.png) | ![image](https://cdn.nlark.com/yuque/0/2022/png/179989/1649387175549-a253a055-bd99-4ef1-b454-af7eb73a670e.png) | ![image](https://cdn.nlark.com/yuque/0/2022/png/179989/1649387180099-b12702b2-65e2-4b8f-bbeb-51f2b2dd1fc6.png) | ![image](https://cdn.nlark.com/yuque/0/2022/png/179989/1649387183911-1924a032-b726-4256-81be-2ffeb30af461.png) |

## 兼容性

当前基础库版本 [2.7.0](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 及以上才支持该组件，在低版本基础库上该组件将不会显示。可通过下述方式判断组件是否支持：

```javascript
if (my.canIUse('error-view')) {
  // 支持使用 error-view 组件
} else {
  // 不支持使用 error-view 组件
}
```
