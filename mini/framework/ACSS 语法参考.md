ACSS 是一种样式语言，用于定义 AXML 组件的样式，从而决定组件的显示效果。

ACSS 与传统的 CSS 规则完全兼容，前端开发者可以无缝使用。为了更好地适应小程序开发，ACSS 还扩展了 CSS，支持 `px`、`rpx`、`vh`、`vw` 等单位。

ACSS 也处理了不同手机端的样式兼容性问题，简化了开发者的工作。

# rpx

`rpx`（responsive pixel）是一种尺寸单位，它能根据屏幕宽度自动进行适配。在小程序中，规定屏幕宽为 750 rpx。以 iPhone6 为例，其屏幕宽度为 375 px，拥有 750 个物理像素，因此 1 rpx 等于 0.5 px，相当于 1 物理像素。

下表展示了不同设备下的 rpx 与 px 的换算关系：

| 设备         | rpx 换算 px（屏幕宽度 / 750） | px 换算 rpx（750 / 屏幕宽度） |
| ------------ | --------------------------- | --------------------------- |
| iPhone5      | 1 rpx = 0.42 px               | 1 px = 2.34 rpx               |
| iPhone6      | 1 rpx = 0.5 px                | 1 px = 2 rpx                  |
| iPhone6 Plus | 1 rpx = 0.552 px              | 1 px = 1.81 rpx               |

# 样式导入

通过使用 `@import` 语句，可以在 ACSS 文件中导入外部样式表。在 `@import` 语句后面，需要指定外联样式表的相对路径，并以分号 `;` 结束该声明。

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

ACSS 支持从 `node_modules` 目录导入第三方模块的样式文件，例如在 `page.acss` 中导入。

```css
@import './button.acss'; /* 相对路径 */
@import '/button.acss'; /* 项目绝对路径 */
@import 'third-party/page.acss'; /* 第三方 npm 包路径 */
```
# 内联样式

在 ACSS 中，可以使用 `style` 和 `class` 属性来控制组件的样式。

## style 属性

`style` 属性用于设置动态样式，这些样式将在运行时被解析。注意，行内样式不支持使用 `!important` 来提升优先级。

**示例代码**：

```html
<view style="color: {{color}};"></view>
```

## class 属性

`class` 属性用于应用静态样式，其值是一个或多个样式类名的集合。类名不需要包含点号 `.` 前缀，并且多个类名之间应以空格分隔。建议将静态样式放在 `class` 中，以避免将静态样式写入 `style` 属性，这样可以提高渲染效率。

**示例代码**：

```html
<view class="my-awesome-view"></view>
```
# 选择器

ACSS 选择器的使用方式与 CSS3 保持一致，提供了丰富的选择器用于定位和样式化页面中的元素。

**注意**：

- 类选择器以 `.a-` 或 `.am-` 开头的是系统组件保留的，开发者应避免使用这些前缀以免发生冲突。
- ACSS 不支持属性选择器。

# 全局样式与局部样式

- 在 `app.acss` 文件中定义的样式是全局样式，这些样式将影响小程序中的所有页面。
- 在页面文件夹内的 `.acss` 文件中定义的样式是局部样式，只影响对应的页面，并且可以覆盖 `app.acss` 中的同名选择器。

# 本地资源引用

在 ACSS 文件中引用本地资源时，应使用绝对路径。相对路径的引用方式不被支持。

**示例代码**：

```css
/* 正确的引用方式 */
background-image: url('/images/ant.png');

/* 错误的引用方式 */
background-image: url('./images/ant.png');
```
# 常见问题

## 一个 axml 引用多个自定义组件或 template 模板、include 等，造成样式之间相互影响、样式污染怎么办？

对于基础库版本小于 2.7.2 的小程序，建议使用类命名空间来处理样式隔离，避免样式冲突。从基础库版本 2.7.2 开始，自定义组件的 JSON 文件中可以配置 `styleIsolation` 选项，这有助于防止页面样式相互影响。

```json
{
  "styleIsolation": "apply-shared"
}
```

`styleIsolation` 支持的选项包括：

- `apply-shared`：表示自定义组件将受到 app.acss 样式以及其他设置了 shared 的页面和自定义组件的样式影响，但自定义组件内部的样式不会影响外部。
- `shared`（默认值）：表示自定义组件的样式既会受到 app.acss 的影响，也可能会影响外部的样式。

## 设置页面高度 100% 没有效果怎么办？

如果设置元素高度为 100% 没有效果，可能是因为其父容器没有设置高度，导致 100% 实际上等于 0。解决方法是确保父容器有明确的高度，或者给元素设置绝对定位。

# 相关文档

更多关于小程序开发的详细信息，请参考[小程序全局配置介绍](https://opendocs.alipay.com/mini/framework/app)。