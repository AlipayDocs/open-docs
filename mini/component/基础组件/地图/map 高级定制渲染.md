# 简介

高级定制渲染是地图组件的能力扩展，使小程序地图具备动态定制地图覆盖物渲染布局的能力。

## 使用限制

- 支付宝版本 10.1.92 及以上，基础库版本[1.23.0](https://opendocs.alipay.com/mini/framework/compatibility) 及以上。
- IDE 模拟器暂不支持调试，请在真机进行相关调试。
- 定制渲染的 XML 布局文件支持编写模板参数，标准是“${参数名称}”，在设置 layout 时可以通过传递 params 参数，地图渲染时会根据传递的模板参数动态渲染。
- 引用的 XML 文件要放在小程序根目录下，不能放在 pages 目录下，否则显示不出来。
- 布局的 XML 文件默认会被 IDE 打包工具忽略，需要在根目录 mini.project.json 配置规则里将 xml 打到小程序中。

```javascript
{
   "include":["**/*.xml"] // 配置包含 xml
}
```

# 使用

高级定制渲染组件的详细能力描述如下：

- 针对 [marker](https://opendocs.alipay.com/mini/component/map#Marker%20%E5%9B%BE%E9%89%B4) 的 icon 图标和 customCallout 气泡进行定制渲染。
- 针对 [marker](https://opendocs.alipay.com/mini/component/map#Marker%20%E5%9B%BE%E9%89%B4) 的 icon 图标进行的定制渲染布局不支持点击事件。
- 针对 [marker](https://opendocs.alipay.com/mini/component/map#Marker%20%E5%9B%BE%E9%89%B4) 的 customCallout 气泡进行定制渲染的布局提供点击事件响应能力。在 calloutTap 事件响应点击事件，此时 data 数据字段会多一个 layoutId 标识事件点击目标，layoutId 即为定制渲染布局中的被点击组件的 ID。
- 以下为渲染前与渲染相对布局后对比图：<br />![](https://mdn.alipayobjects.com/afts/img/A*WA1sQbRh39sAAAAAAAAAAABkAa8wAA/original?bz=openpt_doc&t=ktiPlKDJDWd8L4up4qap_AAAAABkMK8AAAAA#align=left&display=inline&height=279&margin=%5Bobject%20Object%5D&originHeight=279&originWidth=354&status=done&style=none&width=354) ![](https://mdn.alipayobjects.com/afts/img/A*POkaR5JUHxYAAAAAAAAAAABkAa8wAA/original?bz=openpt_doc&t=D4P2DRjYE0PmK07z2U_45AAAAABkMK8AAAAA#align=left&display=inline&height=274&margin=%5Bobject%20Object%5D&originHeight=274&originWidth=324&status=done&style=none&width=324) <br />
- 支持 customCallout 默认气泡样式背景的个性化设置。

## 示例代码

### 布局示例

#### 相对布局

```html
<!--.xml-->
<box>
  <image
    width="60"
    height="60"
    src="https://gw.alipayobjects.com/mdn/rms_a8e3ca/afts/img/A*1NvpQqfbis8AAAAAAAAAAABkARQnAQ"
  />
  <text
    text="X1"
    color="#FFFFFF"
    font-size="8"
    background-color="#FF0000"
    border-radius="6"
    padding-left="3"
    padding-right="3"
    right="0"
  />
</box>
```

效果示例<br />![](https://mdn.alipayobjects.com/afts/img/A*POkaR5JUHxYkUNBPkVeYGQBkAa8wAA/original?bz=openpt_doc&t=cxWtjI5AKA21XOFAVj5CDQAAAABkMK8AAAAA#align=left&display=inline&height=274&margin=%5Bobject%20Object%5D&originHeight=274&originWidth=324&status=done&style=none&width=324)

#### 水平布局

```html
<!--.xml-->
<box layout="horizontal">
  <text
    id="test1"
    clickable="true"
    text="测试1"
    padding-left="8"
    padding-right="8"
    font-size="16"
    border-radius="6"
    background-color="#FF0000"
  />
  <text
    id="test2"
    clickable="true"
    text="测试2"
    padding-left="8"
    padding-right="8"
    font-size="16"
    border-radius="6"
    background-color="#FF0000"
  />
</box>
```

效果示例

![](https://mdn.alipayobjects.com/afts/img/A*xBUiQbeiKEgAAAAAAAAAAABkAa8wAA/original?bz=openpt_doc&t=uvXVk2WyRr7BB4JuIOWvqAAAAABkMK8AAAAA#align=left&display=inline&height=277&margin=%5Bobject%20Object%5D&originHeight=277&originWidth=324&status=done&style=none&width=324)

#### 垂直布局

```html
<!--.xml-->
<box layout="vertical">
  <text
    id="test1"
    clickable="true"
    text="测试1"
    padding-left="8"
    padding-right="8"
    font-size="16"
    border-radius="6"
    background-color="#FF0000"
  />
  <text
    id="test2"
    clickable="true"
    text="测试2"
    padding-left="8"
    padding-right="8"
    font-size="16"
    border-radius="6"
    background-color="#FF0000"
  />
</box>
```

效果示例

![](https://mdn.alipayobjects.com/afts/img/A*lpeWQJuPo-IAAAAAAAAAAABkAa8wAA/original?bz=openpt_doc&t=FmkK9I9pZkbZqTBu7Ih22AAAAABkMK8AAAAA#align=left&display=inline&height=294&margin=%5Bobject%20Object%5D&originHeight=294&originWidth=346&status=done&style=none&width=346)

#### 复杂布局

```html
<!--.xml-->
<box layout="vertical">
  <text text="标题栏" font-size="16" color="#FFFFFF" />
  <box layout="horizontal">
    <text
      id="dh"
      clickable="true"
      text="导航"
      color="#FFFFFF"
      padding-left="8"
      padding-right="8"
      font-size="16"
      border-radius="6"
      background-color="#1591CF"
    />
    <text
      id="xc"
      clickable="true"
      text="相册"
      color="#FFFFFF"
      padding-left="8"
      padding-right="8"
      font-size="16"
      border-radius="6"
      background-color="#1591CF"
    />
    <text
      id="wxt"
      clickable="true"
      text="卫星图"
      color="#FFFFFF"
      padding-left="8"
      padding-right="8"
      font-size="16"
      border-radius="6"
      background-color="#1591CF"
    />
  </box>
</box>
```

效果示例

![](https://mdn.alipayobjects.com/afts/img/A*sYOlTLmKa5UAAAAAAAAAAABkAa8wAA/original?bz=openpt_doc&t=7TOaVpCNzlrcc6AEURSDyQAAAABkMK8AAAAA#align=left&display=inline&height=277&margin=%5Bobject%20Object%5D&originHeight=277&originWidth=324&status=done&style=none&width=324)

### 调用示例

#### .xml 示例代码

```xml
<!-- layout/marker_icon.xml-->
<box>
	<image width='60' height='60' src='https://gw.alipayobjects.com/mdn/rms_a8e3ca/afts/img/A*1NvpQqfbis8AAAAAAAAAAABkARQnAQ'/>
	<text text='X${count}' color='#FFFFFF' font-size='8' background-color='#FF0000'
        border-radius='6' padding-left='3' padding-right='3' right='0'/>
</box>
```

#### .xml 示例代码

```xml
<!-- layout/marker_customcallout.xml-->
<box layout='vertical' background-color='${bgColor}'>
  <text text='${title}' font-size='16' color='#FFFFFF'/>
  <box layout='horizontal'>
    <text id='dh' clickable='true' text='导航' color='#FFFFFF'
          padding-left='8' padding-right='8' font-size='16'
          border-radius='6' background-color='#1591CF'/>
    <text id='xc' clickable='true' text='相册' color='#FFFFFF'
          padding-left='8' padding-right='8' font-size='16'
          border-radius='6' background-color='#1591CF'/>
    <text id='wxt' clickable='true' text='卫星图' color='#FFFFFF'
          padding-left='8' padding-right='8' font-size='16'
          border-radius='6' background-color='#1591CF'/>
  </box>
</box>
```

#### .js 示例代码

```javascript
// marker数据
const markers = [
  {
    id: 5,
    latitude: 30.275052,
    longitude: 120.140716,
    width: 60,
    height: 60,
    iconLayout: {
      params: {
        count: '1',
      },
      src: '/layout/marker_icon.xml',
    },
    customCallout: {
      canShowOnTap: true,
      layout: {
        params: {
          title: '标题栏',
          bgColor: '#FF00FF',
        },
        src: '/layout/marker_customcallout.xml',
      },
      layoutBubble: {
        style: 'bubble',
        bgColor: '#898986',
        borderRadius: 0,
      },
    },
  },
];
```

## 通用属性

下面所呈列的所有属性均适用于高级定制渲染组件。

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| id | String | 元素标识。<br />**说明：** 不要设置为 0，否则会出现获取为空现象。 |
| width | Number | 元素的宽度。 |
| height | Number | 元素的高度。 |
| left | Number | 元素的左侧外边距。<br />**默认值：** 0 |
| top | Number | 元素上方的外边距。<br />**默认值：** 0 |
| right | Number | 元素的右侧外边距。 |
| bottom | Number | 元素下方的外边距。 |
| background-color | String | 元素的背景颜色。<br />**默认值：** #00000000 |
| padding | Number | 元素的所有内边距。<br />**默认值：** 0 |
| padding-left | Number | 元素的左侧内边距。<br />**默认值：** 0 |
| padding-top | Number | 元素上方的内边距。<br />**默认值：** 0 |
| padding-right | Number | 元素的右侧内边距。<br />**默认值：** 0 |
| padding-bottom | Number | 元素下方的内边距。<br />**默认值：** 0 |
| border-color | String | 元素的边框颜色。<br />**默认值：** #00000000 |
| border-radius | Number | 元素的圆角边框圆角半径。<br />**默认值：** 0 |
| border-width | Number | 元素的边框宽度。<br />**默认值：** 0 |

customCallout 气泡背景个性化设置 layoutBubble 属性说明

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| style | String | 设置气泡边框，默认带气泡背景。设置为 none 时，隐藏背景。<br />**默认值：** bubble |
| bgColor | String | 气泡背景色。 |
| borderRadius | Number | 气泡圆角设置。 |

## 组件

地图高级定制渲染组件包含 box（区域）、text（文本）、image（图片）、lottie（动画）。

### box

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| layout | String | 布局类型：<br /><ul><li>relative：相对布局</li><li>horizontal：水平布局</li><li>vertical：垂直布局、复杂布局</li></ul> **注意：** iOS 在 10.1.92 以下版本不支持 horizontal 和 vertical。<br />**默认值：** relative |
| horizontal-align | String | 子元素水平对齐方式，有效值：middle。 |
| vertical-align | String | 子元素垂直对齐方式，有效值：middle。 |

### text

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| text | String | 文本内容。 |
| color | String | 文本颜色。<br />**默认值：** #00000 |
| font-size | Number | 文本字体大小。 |
| clickable | Boolean | 文本是否可点击响应事件。<br />**默认值：** false |
| number-of-lines | Number | 文本最大显示行数。 |
| stroke-color | String | 文本文字描边颜色。<br />**默认值：** #FFFFFFFF |
| stroke-width | Number | 文本文字描边宽度。 |
| text-align | String | 文本对齐方式。有效值：left、center、right。<br />**默认值：** left |
| font-weight | String | 文本字体粗细程度。有效值：normal、bold。<br />**默认值：** nomal |

### image

支持：

- 绝对路径：如 'https://gw.alipayobjects.com/XXX'
- 相对路径（基准为根目录）：如 /img/testPic.png

**注意：** 相对路径不支持 ./img/testPic.png 方式。

| **属性**    | **类型** | **描述**     |
| ----------- | -------- | ------------ |
| src         | String   | 图片路径。   |
| placeholder | String   | 占位图路径。 |

### lottie

| **属性** | **类型** | **描述**   |
| -------- | -------- | ---------- |
| src      | String   | 动画路径。 |
