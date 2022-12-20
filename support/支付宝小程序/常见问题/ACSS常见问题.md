## 使用说明
- 选择器同 CSS3 保持一致。
- `.a-`, `.am-` 开头的类选择器为系统组件占用，不可使用。
- 不支持属性选择器。 

## 常见问题

### rpx与px单位相互换算
参考[rpx与px单位相互换算](https://opendocs.alipay.com/support/01rb6o)。 

### acss文件内图片路径
小程序的acss文件内图片不支持使用相对路径，可以使用绝对路径或使用网络图片 URL 地址。 

### 小程序是否支持CSS3动画
ACSS 支持 css3 动画。支付宝小程序中有提供动画的 API，详细参考 [my.createAnimation](https://opendocs.alipay.com/mini/api/ui-animation)。 

### 小程序支持css3中的::before、calc、vh、vw吗
小程序 acss 支持::before、calc、vh、vw。 

### 小程序acss支持attr属性吗
小程序 acss 不支持 attr 属性。 

### 小程序如何引入样式
小程序中不支持引入在线样式，项目内其它 css 样式可通过 @import 从其它样式表导入样式规则。公共样式需要在小程序根目录下的 app.acss 中进行编辑。 

### 小程序如何引用外部字体？
小程序引入外部字体请在小程序 acss 文件中利用 css3 的 font-face 进行引入，或者使用动态加载网络字体 [my.loadFontFace](https://opendocs.alipay.com/mini/api/ggawf0)。 

### 大数据列表页面做a:if切换隐藏，UI卡顿
可建议使用 view 的 hidden 属性来实现大数据列表在单个页面中的显示隐藏效果。会更加流畅。 

### 处理axml引用多个自定义组件或模板等造成样式之间相互影响
需要开发者自行通过名空间处理样式隔离。 

### 小程序如何显示每行显示bottom虚线框inline样式的底部border
可以使用 css 样式实现方式直接实现：border-bottom: 1px dashed #999;display: inline; 

### rpx自动转换成px或rem的规则
rpx 自动转换成 px 或 rem 的规则：通过 acss 设置的样式转成 rem，通过 style 设置的样式转成 px。 

### button按钮默认样式如何去除
在小程序当前页面的 page.acss 里添加样式清除或者在 app.acss 里添加，参考以下代码：<br />
**注意：** 在 app.acss 里添加，所有 button 都会改。
```css
button {  
  background-color: transparent;  
  padding: 0;  
  margin: 0;  
  position: static;
  border: 0; 
  border-radius: 0;
  color: transparent;}
button::after { 
  content: ''; 
  width: 0; 
  height: 0; 
  -webkit-transform: scale(1); 
  transform: scale(1); 
  display: none; 
  background: transparent;}
```

