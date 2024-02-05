[openvideo-axml 介绍](https://gw.alipayobjects.com/v/portal_cjapev/afts/video/A*jrdoTagCX1sAAAAAAAAAAAAAAQAAAQ)

AXML 是小程序框架设计的一套标签语言，结合基础组件和事件系统，可以构建出小程序页面的结构。AXML 语法可分为五个部分：[数据绑定](https://opendocs.alipay.com/mini/framework/data-binding)、[条件渲染](https://opendocs.alipay.com/mini/framework/conditional-render)、[列表渲染](https://opendocs.alipay.com/mini/framework/list-render)、[模板](https://opendocs.alipay.com/mini/framework/axml-template)、[引用](https://opendocs.alipay.com/mini/framework/import)。

# 数据绑定

## AXML 示例代码

```html
<!-- axml -->
<view>{{ message }}</view>
```

## .js 示例代码

```javascript
// page.js
Page({
  data: {
    message: 'Hello World'
  }
});
```

## 效果示例

![](https://cdn.nlark.com/yuque/0/2022/png/179989/1660805803075-4df8eb16-58e7-463c-9c2f-ae6e862cc9e6.png)
# 列表渲染

## AXML 示例代码

```html
<!-- axml -->
<view a:for="{{list}}">{{item}}</view>
```

## .js 示例代码

```javascript
// page.js
Page({
  data: {
    list: [1, 2, 3, 4, 5]
  }
});
```

## 效果示例

![](https://cdn.nlark.com/yuque/0/2022/png/179989/1660805811400-c7379ce5-1026-43eb-8aa2-10f39922a087.png)
# 条件渲染

## AXML 示例代码

```html
<!-- axml -->
<view a:if="{{view == 'WEBVIEW'}}"> WEBVIEW </view>
<view a:elif="{{view == 'APP'}}"> APP </view>
<view a:else> ALIPAY </view>
```

## .js 示例代码

```javascript
// page.js
Page({
  data: {
    view: 'ALIPAY',
  },
});
```

## 效果示例

![](https://cdn.nlark.com/yuque/0/2022/png/179989/1660805818878-f36efae3-5fed-4362-9cee-1f8da95569c2.png)
# 模板

## AXML 示例代码

```html
<!-- axml -->
<template name="taskTpl">
  <view class="task-item">
    <text class="desc">{{taskDescription}}</text>
    <text class="time">{{deadline}}</text>
  </view>
</template>

<template is="taskTpl" data="{{ ...taskA }}"></template>
<template is="taskTpl" data="{{ ...taskB }}"></template>
```

## .js 示例代码

```javascript
// page.js
Page({
  data: {
    taskA: {
      taskDescription: '学习支付宝小程序',
      deadline: '2022-09-15',
    },
    taskB: {
      taskDescription: '读完《三国演义》',
      deadline: '2022-10-15',
    },
  },
});
```

## 效果示例

![](https://cdn.nlark.com/yuque/0/2022/png/179989/1660805824958-94f8a2ee-9262-4693-80e8-259604c04ed8.png)
