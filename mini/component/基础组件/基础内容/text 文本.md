# 简介

文本。

## 扫码体验

![|127x157](https://gw.alipayobjects.com/zos/skylark/b4c189f1-22d5-4832-9080-5c786ab589fd/2018/jpeg/3b380081-14e7-43a2-a4b2-17ae32d50d6f.jpeg#align=left&display=inline&height=1906&margin=%5Bobject%20Object%5D&originHeight=1906&originWidth=1540&status=done&style=none&width=127)

# 使用

## 在线示例

[小程序在线](https://opendocs.alipay.com/openbox/mini/opendocs/basic-component?view=preview&defaultPage=pages/text/index&defaultOpenedFiles=pages/text/index&theme=light)

## 属性说明

| 属性         | 类型    | 描述                                                      |
| ------------ | ------- | --------------------------------------------------------- |
| selectable   | Boolean | 是否可选。**默认值：** false                              |
| space        | String  | 以何种方式显示连续空格。                                  |
| decode       | Boolean | 是否解码。为 true 时表示对文本内容进行解码，可解析的 HTML 实体字符有：`&nbsp;`、`&lt;`、`&gt;`、`&amp;`、`&apos;`、`&ensp;`、`&emsp;`。**默认值：** false |
| number-of-lines | Number | 多行省略，值须大于等于 1，表现同 css 的 `-webkit-line-clamp` 属性一致。 |

### space 有效值

**说明：** 各个操作系统的空格标准并不一致。

| 属性 | 描述             |
| ---- | ---------------- |
| nbsp | 根据字体设置的空格大小。 |
| ensp | 中文字符空格一半大小。   |
| emsp | 中文字符空格大小。       |
