## 报错描述
小程序使用 [my.paySignCenter](https://opendocs.alipay.com/mini/006v6d) 唤起周期扣款签约时报无效签名。

## 报错原因

- 密钥错误。
- 入参可能存在乱。
- my.paySignCenter 唤起签约时没有对服务端生成的字符串进行编码。

## 解决方案

1. 检查密钥和入参是否错误，可查看 [isv.invalid-signature（无效签名）](https://opendocs.alipay.com/support/01rax2)进行排查。
2. 对服务端生成的签约字符串进行编码。
```javascript
  paySignCenter() {
    my.paySignCenter({   
      //对服务端返回的签约字符串进行urlencode编码（如果服务端已进行编码则不需要再进行编码） 
      signStr: encodeURIComponent('服务端返回的签约字符串'), 
      success: (res) => {
        my.alert({      
          title: 'success', // alert框的标题content: JSON.stringify(res),    
        })    
      },     
      fail: (res) => {  
        my.alert({       
          title: 'fail', // alert框的标题      
          content: JSON.stringify(res),      
        })   
      },  
    })          
```

