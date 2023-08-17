## 说明

### a:key

- 如不提供 a:key，会报一个 warning。
- 如果明确知道列表是静态，或者不用关注其顺序，则可以忽略。
- key 不能设置在 block 上。

### template
template 的子节点只能是一个。

## 常见问题

### rpx与px单位相互换算
参考[rpx与px单位相互换算](https://opendocs.alipay.com/support/01rb6o)。 

### 小程序适配iphoneX介绍
参考[小程序适配iphoneX介绍](https://opendocs.alipay.com/support/01rb0b)。 

### 小程序点击事件如何传参
参考[小程序点击事件如何传参](https://opendocs.alipay.com/support/01rb3d)。 

### Android小程序页面刘海屏适配
参考[Android小程序页面刘海屏适配](https://opendocs.alipay.com/support/01rb0g)。 

### 小程序是否支持webp图片

- 小程序支持 webp 格式图片，如果 webp 格式图片显示不出来，可以咨询对应提供图片服务的服务端。
- Android 支持 webp 格式动图，iOS 本身就不支持 webp 格式动图。

### 小程序引用
axml 提供两种文件引用方式 import 和 include。

- import。import 可以加载已经定义好的 template。
- include。include 可以将目标文件除 <template/> 外整个代码引入，相当于是拷贝到 include 位置。
- 引入路径。模板引入路径支持相对路径、绝对路径，也支持从 node_modules 目录载入第三方模块。

参考文档：[axml-引用](https://opendocs.alipay.com/mini/framework/import)。

### 小程序阻止事件冒泡
以关键字 on 为前缀的事件都是[冒泡事件](https://opendocs.alipay.com/mini/framework/events)，想要阻止冒泡可以使用以关键字 catch 为前缀的非冒泡事件来阻止。<br />使用关键字 catch 为前缀的非冒泡事件来阻止事件冒泡。  

### axml文件中能使用JS函数吗
不可以，axml 可以在数据绑定时做逻辑运算，不能调用 JS 函数。 

### template模板可以用自定义组件吗
template 中不能使用自定义组件。 

### template的is属性有什么做用
模板 [template](https://opendocs.alipay.com/mini/framework/axml-template) 的 is 属性可以使用 Mustache 语法，来动态决定具体渲染哪个模板。 

### 条件渲染，对比 a:if 与 hidden

- a:if 中的模板可能包含数据绑定，所以当 a:if 的条件值切换时，框架有局部渲染的过程，用于确保条件块在切换时销毁或重新渲染。此外， a:if 在初始渲染条件为 false 时，不触发任何渲染动作，当条件第一次变成 true 时才开始局部渲染。
- hidden 控制显示与隐藏，组件始终会被渲染。

**注意：** 一般来说，a:if 有更高的切换消耗而 hidden 有更高的初始渲染消耗。因此，在需要频繁切换的情景下，用 hidden 更好。如果在运行时条件改变不多则 a:if 较好。 

### 页面白屏报错：系统错误，请稍后重试

- 这是 render 层的报错，开发工具的调试器看不到错误日志。
- 系统错误，请稍后重试！一般是显示页面的 axml 渲染数据异常导致，可以侧重排查下显示页面的渲染数据，例如直接渲染了 {{object}}、{{objectArray}} 等引用类型数据；引用类型的数据渲染时应该指定到具体的属性值， 例如：{{object.name}}、{{objectArray[arrIndex].name}}。 
- 如果页面有使用 picker 组件，。<br />**注意：** range的数据类型，如果是 Object[]，必须要指定 range-key；picker 内指定当前选择项时，要指到具体的数据， 例如：{{objectArray[arrIndex].name}}。 

### axml中数据绑定时如何避免对-符号属性的解析
**问题描述：**<br />axml中，style 动态设置样式如果属性里带有'-'将会报错，如何避免对'-'的解析。<br />代码：
```
<view class="fi-title" style="{{margin:titleMargin?titleMargin:'0 0 8px 0'}}">title</view> <view class="fi-title" style="{{margin-bottom:titleMargin?titleMargin:'10px'}}">title</view>
```
代码中<br />
**margin：** style="{{margin:titleMargin?titleMargin:'0 0 8px 0'}}"正常；<br />
**margin-bottom：** style="{{margin-bottom:titleMargin?titleMargin:'10px'}}"报错。<br />
**原因分析：** {{}}是数据绑定时使用，{{}}内的属性会被认作变量来进行数据传递，变量的写法不支持-符号，所以会导致报错。<br />
**解决方案：** 样式属性名放在{{}}外，只对动态数值变量做逻辑判断处理即可。如：
```
<view class="fi-title" style="margin-bottom:{{titleMargin?titleMargin:'10px'}}" >title</view>
```

### 事件的函数能像JS一样传参吗
不支持。可以使用data-*自定义属性实现传参。<br />示例：
```json
<view data-test="1" onTap="onTap"> DataSet Test </view>
```
```javascript
Page({
  onTap(e) {
      console.info(e.currentTarget.dataset.test);
  }})
```

### 如何动态修改class样式

1. 通过三元运算符实现：
```javascript
<view class="{{条件表达式 ? 'classA' : 'classB'}}"></view>
```

2. 通过 setData 动态修改样式，但只能使用 style 行内样式实现：
```javascript
<view class="{{条件表达式 ? 'classA' : 'classB'}}"></view>
```
```json
Page({
    data:{
        width:'',      
        height:''
            },
    onLoad(){
         my.getSystemInfo({
             //获取手机系统信息，如窗口高度与宽度
            success:(res)=>
                  this.setData({
                    width:res.windowWidth ,         
                    height:res.windowHeight
                  })         
         }
         })       
    }
})
```
 
