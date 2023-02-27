通过三元运算符实现：
```html
<view class="{{条件表达式 ? 'classA' : 'classB'}}"></view>
```
通过 setData 动态修改样式，但只能使用 style 行内样式实现：
```html
<view style="width:{{width};height:{{height}}}"></view>
```
```javascript
Page({   
  data:{    
    width:'',    
    height:''
  },onLoad(){   
    my.getSystemInfo({     
      //获取手机系统信息，如窗口高度与宽度   
      success:(res)=>{         
        this.setData({           
          width:res.windowWidth ,  
          height:res.windowHeight 
        })       
      }      
    })     
  }})
```
 
