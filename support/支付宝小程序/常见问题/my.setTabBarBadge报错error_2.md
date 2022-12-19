## 错误码
error:2 

## 问题描述
小程序调用my.setTabBarBadge为标签页（tabbar）某一项的右上角添加文本。报错 {"errorMessage":"you should specify index or tag!","message":"you should specify index or tag!","error":2}。 

## 涉及接口
[my.setTabBarBadge](https://opendocs.alipay.com/mini/api/qm7t3v)

## 报错原因
index 参数名和参数值入参有误或为空导致。 

## 解决方案

- 确认 index 参数名是否编写正确和入参。
- 确认 index 入参值是否为正确的标签页（tabbar）项数序号（从左边以0开始计数）。
- 如果是模拟器报错 **参数无效**，请使用真机预览调试，模拟器目前不支持模拟该API。

### 示例代码
```html
my.setTabBarBadge({ 
  index: 0,//表示设置左边开始第一个tabbar标签页 
  text: '42'
})
```
 
