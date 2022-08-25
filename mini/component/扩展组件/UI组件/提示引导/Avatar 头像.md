# 简介

头像。

## 扫码体验

![|154x191](https://mdn.alipayobjects.com/afts/img/A*wQu2TLea8JsAAAAAAAAAAABkAa8wAA/original?bz=openpt_doc&t=ezrdO7s0f2889e0cDyjjIAAAAABkMK8AAAAA#align=left&display=inline&height=191&margin=%5Bobject%20Object%5D&originHeight=191&originWidth=154&status=done&style=none&width=154)

# 使用

## Herbox

[小程序在线](https://herbox-embed.alipay.com/s/doc-aliui-avatar?theme=light&previewZoom=75&chInfo=openhome-doc)

## 示例代码

### .json 示例代码

```json
{
  "defaultTitle": "Avatar",
  "usingComponents": {
    "avatar": "mini-ali-ui/es/avatar/index"
  }
}
```

### .axml 示例代码

```html
<view>
  <!--普通头像组件-->
  <avatar src="xxxx" shape="standard" />
  <!--带用户名和摘要描述头像组件-->
  <avatar src="xxxx" size="lg" name="用户名" desc="摘要描述" shape="standard" />
</view>
```

## 属性说明

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| className | String | 自定义 class。 |
| src | String | 头像图片资源地址。<br />**默认值：** 默认蓝底头像 |
| size | String | 头像尺寸大小。<br />**可选值：** lg、md、sm、xs。<br />**默认值：** md<br />**版本要求**：mini-ali-ui [1.2.0](https://www.npmjs.com/package/mini-ali-ui?activeTab=versions) 及以上 |
| shape | String | 头像形状。可选值：standard、circle、square。<br />**默认值：** circle<br />**版本要求**：mini-ali-ui [1.2.0](https://www.npmjs.com/package/mini-ali-ui?activeTab=versions) 及以上 |
| name | String | 设置用户名。 |
| desc | String | 设置摘要信息。 |
| onError | EventHandle | 图片资源加载失败回调<br />**默认值：** (e: Object) => void |
