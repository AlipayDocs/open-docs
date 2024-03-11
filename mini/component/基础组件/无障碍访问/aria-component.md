# 简介

`aria` 属性是 [WAI-ARIA](https://www.w3.org/TR/wai-aria/) 标准提供无障碍访问动态、可交互 Web 内容的技术规范。从基础库 `1.18.0` 版本开始，小程序框架的部分基础组件支持 `aria` 属性，能够满足视障人士对于小程序的无障碍访问需求。

## 使用限制

- 支持 `aria` 属性的小程序组件包括：[view](https://opendocs.alipay.com/mini/component/view)、[text](https://opendocs.alipay.com/mini/component/text)、[icon](https://opendocs.alipay.com/mini/component/icon)、[button](https://opendocs.alipay.com/mini/component/button)、[label](https://opendocs.alipay.com/mini/component/label)、[checkbox](https://opendocs.alipay.com/mini/component/checkbox)、[switch](https://opendocs.alipay.com/mini/component/switch)、[image](https://opendocs.alipay.com/mini/component/image) 和 [radio](https://opendocs.alipay.com/mini/component/radio)。
- **Native 渲染引擎**：暂不支持。

# 使用

## 常用 `aria` 属性

### role

`aria` 属性的核心是 `role` 属性，该属性代表组件的语义角色。例如，当 `role` 属性设置为 `img` 时，组件获得焦点后读屏软件会朗读 **图像**；设置为 `button` 时，获得焦点后读屏软件会朗读 **按钮**。

```html
<view class="button" onTap="defaultTap" role="button" aria-label="确定按钮"
  >确定按钮</view
>
```

示例中的按钮用 `view` 组件实现，`role` 属性让该 `view` 组件承担按钮的语义。当读屏软件聚焦该 `view` 组件时，它会识别出这是一个按钮，朗读 **按钮 确定按钮**。由于小程序采用 AXML 语言，它失去了 HTML 中许多具有语义的标签，如 `h1`、`article`、`header` 等。这些标签与读屏软件配合时，可以传递更丰富的信息给用户。在小程序中，开发者可通过 `role` 属性增强 `view` 组件的语义，以实现类似使用 HTML 标签的效果。例如，一篇文章的 HTML 示例代码：

```html
<article>
  <h1>文章标题</h1>
  <h2>第一章</h2>
  <p>第一段落⋯⋯</p>
</article>
```

即使小程序没有 `article`、`h1`、`h2` 等对应的组件，利用带有 `role` 属性的 `view` 组件，同样可以实现效果。例如：

```html
<view role="article">
  <view role="heading" aria-level="1">文章标题</view>
  <view role="heading" aria-level="2">第一章</view>
  <view>第一段落⋯⋯</view>
</view>
```

当读屏软件聚焦到 **文章标题** 的 `view` 组件时，会朗读 **文章标题 标题 1**；聚焦到 **第一章** 的 `view` 组件时，会朗读 **第一章 标题 2**。其中 **标题** 是 `role` 提供的语义信息，**2** 则由 `aria-level` 属性设定。`aria-level` 属性是 `aria` 属性中的一种，它提供附加信息，如示例中的 `aria-level` 表明标题的级别。部分 `role` 属性的值必须与其他 `aria` 属性结合使用才能生效。例如，`role="img"` 时必须配置 `aria-label` 属性，否则读屏软件会忽略 `role` 属性。
### aria-label

`aria-label` 可以代替组件内的文本内容，例如：

```html
<view aria-label="aria-label内容">组件文本内容</view>
```

当聚焦到此处时，读屏软件会朗读出 **aria-label** 内容，而组件内原有的文本内容会被忽略。`aria-label` 还可以配合不带文本内容的组件使用，表示该组件附带的文本信息，聚焦后系统会自动朗读出来。例如 `image` 组件，可以使用 `aria-label` 增添图片的描述信息。

```html
<image src="{{src}}" role="img" aria-label="风景画" />
```

`aria-label` 也适用于使用 `role` 属性的 `view` 组件，例如：

```html
<view style="background-image:url(./bg.jpg);" role="img" aria-label="风景画"></view>
```

对于视觉效果较强的组件（如 `image`），仅让读屏软件朗读出语义，对视障用户意义不大。通过 `aria-label` 属性对这些组件的内容提供文字说明，朗读出的内容会变得更完整，效果更佳。

### aria-labelledby

一些组件和其他组件是有关联的，需要一起朗读才能表达出完整的含义。例如 `checkbox` 组件，往往需要一个 `text` 或 `view` 组件承载该 `checkbox` 选中的文字内容。此时可用 `aria-labelledby` 属性关联两个组件，读屏软件会在读完当前组件的内容后，继续朗读 `aria-labelledby` 指向的组件中的内容。

```html
<label>
  <checkbox aria-labelledby="content" />
  <text id="content">复选框内容</text>
</label>
```

示例中的 `checkbox` 组件获得焦点之后，读屏软件会朗读出“未选中 复选框内容 复选框”。`aria-labelledby` 的值是其他组件的 `id` 属性，组件 `id` 属性必须是独一无二的，列表渲染的时候请勿给组件设置重复的 `id`。
### aria-checked

`aria-checked` 表示 checkbox、switch 等组件是否被选中。聚焦到这些组件后，读屏软件将朗读组件的选中状态“未选中”或者“已选中”，告诉用户当前组件的选中状态。小程序原生组件已预内置了该属性，例如：

```html
<label>
  <checkbox aria-labelledby="content" value="{{checked}}" />
  <text id="content">复选框内容</text>
</label>
```

若使用[自定义组件](https://opendocs.alipay.com/mini/framework/custom-component-overview)开发的 checkbox、switch 等组件，需要使用 `aria-checked` 属性，才能使得读屏软件获取组件选中状态。例如，一个自定义 checkbox 组件的 axml 示例代码：

```html
<view
  class="my-checkbox"
  role="checkbox"
  onTap="handleTap"
  aria-checked="{{checked}}"
  aria-labelledby="myCheckboxText"
>
  <icon type="{{checked ? 'success' : 'clear'}}" size="12" />
  <text id="myCheckboxText">
    <slot></slot>
  </text>
</view>
```

示例中，设置 `my-checkbox` 组件 `role` 属性的值为 `checkbox`，并将组件的选中状态 `checked` 赋值给 `aria-checked` 属性，当读屏软件聚焦到该自定义组件时，可以朗读出该组件的选中信息。该属性也同样适用于 switch、radio 等组件。

### aria-expanded

`aria-expanded` 表示可折叠的组件的展开信息，适合对有折叠功能的组件使用，如折叠菜单、带折叠的下拉菜单等。使用 `aria-expanded` 属性，可让读屏软件朗读组件的展开状态。

## 其他 aria 属性

了解更多 aria 属性可以查看[WAI-ARIA](https://www.w3.org/TR/wai-aria/)。
# 相关信息

无障碍一词来自英文 Accessibility ，是指任何人（无论是健全人、残疾人，还是老年人、孩子）可在任何时候、任何场景使用或者访问。标准化组织（如 [W3C](https://www.w3.org/)、[WAI](https://www.w3.org/WAI/)）制定了 WEB 领域无障碍的标准，支付宝小程序依据现有标准，提供了支付宝小程序无障碍访问功能。

## 无障碍标准

[Web 内容无障碍指南（WCAG）](https://www.w3.org/Translations/WCAG21-zh/) 是由研究无障碍的专家制定的一组指导原则和最佳实践，目的在于有条理地向大家阐释无障碍性的含义和最佳实践。<br />[可访问富互联网应用（WAI-ARIA）](https://www.w3.org/TR/wai-aria/) 是一个为残疾人士等提供无障碍访问动态、可交互 Web 内容的技术规范，为浏览器、媒体播放器、辅助技术的开发人员以及 Web 内容开发者定义了可以获得更广泛跨平台可访问性的方法。<br />小程序的无障碍功能支持 [WAI-ARIA](https://www.w3.org/TR/wai-aria/) 部分属性，开发者可以配合 [WCAG](https://www.w3.org/Translations/WCAG21-zh/)中总结的最佳实践，开发出更易为广大有无障碍需求人士使用的小程序。

## 启动视觉无障碍功能

iOS 系统和 Android 系统提供了视觉无障碍特性，为盲人或视力不佳的用户提供读屏功能，能够朗读出用户所触摸、选择、激活的内容。

- iOS：**设置 > 通用 > 辅助功能 > VoiceOver**，开启 VoiceOver（旁白）功能。<br />
- Android：Android 系统的读屏功能名为 **TalkBack**，将其开启即可。（不同品牌的 Android 手机中，开启 TalkBack 功能的位置不一样，请根据手机对应的帮助手册查找 TalkBack 功能的开启方式。）<br />

在开启语音读屏功能的手机中，读屏功能聚焦到小程序的组件时，会朗读出组件的内容。
