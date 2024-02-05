ACSS 是一套样式语言，用于描述 AXML 的组件样式，决定 AXML 组件的显示效果。

为适应广大前端开发者，ACSS 和 CSS 规则完全一致，100% 可以用。同时，为更适合开发小程序，对 CSS 进行了扩充，ACSS 支持 `px`，`rpx`，`vh`，`vw` 等单位。

ACSS 已经帮开发者做了不同手机端的样式兼容性处理。

# rpx

rpx（responsive pixel）是根据屏幕宽度自适应的像素单位，规定屏幕宽为 750rpx。以 Apple iPhone6 为例，屏幕宽度为 375px，共有 750 个物理像素，则 750 rpx = 375 px = 750 物理像素，1 rpx = 0.5 px = 1 物理像素。

| 设备         | rpx 换算 px（屏幕宽度 / 750） | px 换算 rpx（750 / 屏幕宽度） |
| ------------ | ----------------------------- | ----------------------------- |
| iPhone5      | 1 rpx = 0.42 px               | 1 px = 2.34 rpx               |
| iPhone6      | 1 rpx = 0.5 px                | 1 px = 2 rpx                  |
| iPhone6 Plus | 1 rpx = 0.552 px              | 1 px = 1.81 rpx               |

# 样式导入

使用 `@import` 语句可以导入外联样式表，`@import` 后面需要加上外联样式表的相对路径，用分号（`;`）表示结束。

**示例代码**：

```css
/** button.acss **/
.sm-button {
  padding: 5px;
}
```

```css
/** app.acss **/
@import './button.acss';
.md-button {
  padding: 15px;
}
```

导入路径支持从 node_modules 目录载入第三方模块，例如 third-party/page.acss。

```css
@import './button.acss'; /* 相对路径 */
@import '/button.acss'; /* 项目绝对路径 */
@import 'third-party/page.acss'; /* 第三方 npm 包路径 */
```
# 内联样式

组件上支持使用 `style`、`class` 属性来控制样式。

## style 属性

用于接收动态样式，样式在运行时会进行解析。行内样式不支持 `!important` 优先级规则。

```html
<view style="color: {{color}};" />
```

## class 属性

用于接收静态样式，属性值是样式规则中类选择器名（样式类名）的集合，样式类名不需要带上 `.`，多个类名间以空格分隔。请将静态样式写进 class 中，避免将静态样式写进 style 中，以免影响渲染速度。

```html
<view class="my-awesome-view" />
```

# 选择器

同 CSS3 保持一致。

**注意**：

- `.a-`、`.am-` 开头的类选择器为系统组件占用，不可使用。
- 不支持属性选择器。

# 全局样式与局部样式

- `app.acss` 中的样式为全局样式，作用于每一个页面。
- 页面文件夹内的 `.acss` 文件中定义的样式为局部样式，只作用在对应的页面，并会覆盖 `app.acss` 中相同的选择器。

# 本地资源引用

ACSS 文件里的本地资源引用请使用绝对路径的方式，不支持相对路径引用。例如下方示例。

```css
/* 支持 */
background-image: url('/images/ant.png');
/* 不支持 */
background-image: url('./images/ant.png');
```
# 常见问题

## Q：一个 axml 引用多个自定义组件或 template 模板、include 等，造成样式之间相互影响、样式污染怎么办？

A：对于基础库版本小于 `2.7.2` 的小程序，可使用 class 命名空间处理样式隔离。从基础库版本 `2.7.2` 开始，可以在自定义组件的 `JSON` 文件中配置 `styleIsolation`，避免页面的样式影响到外部。例如：

```json
{
  "styleIsolation": "apply-shared"
}
```

该选项支持以下取值：

- `apply-shared` 表示 `app.acss` 样式以及其他设置了 `shared` 的页面和其他自定义组件的样式将影响到自定义组件，而自定义组件 `ACSS` 中定义的样式不会影响外部。
- `shared`（默认）表示 `app.acss` 样式以及其他设置了 `shared` 的页面和其他自定义组件的样式将影响到页面，而自定义组件 `ACSS` 中指定的样式也会影响到外部。

## Q：设置页面高度 `100%` 为什么没用？

A：设置为 `100%` 时，需要依赖父容器的高度。如果父容器没有高度，那么 `100%` 实际上就是 `0`。另外，也可以通过添加绝对定位解决问题。如果不添加绝对定位，页面的高度将会自适应内容的大小。

# 相关文档

[小程序全局配置介绍](https://opendocs.alipay.com/mini/framework/app)
