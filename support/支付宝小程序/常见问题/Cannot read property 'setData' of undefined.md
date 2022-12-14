## 报错描述
在 API 异步回调函数中使用 this 调用 Page 的变量和函数，报错 undefined。<br />例如：在 my.requset 成功回调函数 success 中 this.setData({}) 赋值，直接报：**Uncaught TypeError: Cannot read property 'setData' of undefined**。<br />![](https://gw.alipayobjects.com/zos/sptworksff_prod/dad053c1-a782-41f5-87df-d838cd513ac7.png#align=left&display=inline&height=121&margin=%5Bobject%20Object%5D&originHeight=121&originWidth=636&status=done&style=none&width=636)

## 报错原因
this 指向改变导致，在异步回调函数中 this 不是指向页面 Page，而是指向回调函数局部，所以 this 找不到 Page 的变量或函数报错。

## 解决方案

- 异步回调函数中使用 this，需要在外部重新定义一个 let that=this 然后使用 that.setData({}) 进行数据的赋值。<br />
```javascript
data: {
  setValue:"", 
},  
  onReady(e) { //重新定义thislet 
    that=this;
    my.request({ 
      url: 'https://httpbin.org/post', 
      method: 'POST', 
      data: {   
        from: '支付宝',  
        production: 'AlipayJSAPI', 
      },  
      headers:{  
        'content-type':'application/json'  //默认值 
      }, 
        dataType: 'json', 
      success: function(res) { 
        my.alert({content: 'success'});  
        that.setData({  
          setValue:"重新定义this success"  
        }) 
      }, 
      fail: function(res) {
        my.alert({content: 'fail'}); 
      }, 
      complete: function(res) { 
        my.hideLoading(); 
        my.alert({content: 'complete'});  
      }});
  }
```

- 使用回调箭头函数写法，这样就不存在 this 指向问题，直接使用 this.setData({}) 进行数据的赋值。
```javascript
data: {  
  setValue:"",  
},  
  onReady(e) {//箭头函数 不存在this指向问题
    my.request({  url: 'https://httpbin.org/post',  
                method: 'POST', 
                data: {   
                  from: '支付宝', 
                  production: 'AlipayJSAPI', 
                }, 
                headers:{  
                  'content-type':'application/json'  //默认值 
                }, 
                dataType: 'json', 
                success :(res)=>{  
                  my.alert({content: 'success'});  
                  this.setData({    
                    setValue:"箭头函数success"   
                  }) 
                }, 
                fail: function(res) {   
                  my.alert({content: 'fail'});
                }, 
                complete: function(res) {  
                  my.hideLoading();   
                  my.alert({content: 'complete'});
                }});
  }
```

