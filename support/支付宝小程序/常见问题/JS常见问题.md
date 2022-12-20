### 如何防止连续快速点击事件
参考[如何防止连续快速点击事件](https://opendocs.alipay.com/support/01rb7r)。 

### 小程序如何使用store状态管理
参考[小程序如何使用store状态管理](https://opendocs.alipay.com/support/01rb24)。 

### 小程序JS如何使用正则表达式
参考[小程序JS如何使用正则表达式](https://opendocs.alipay.com/support/01rb7a)。 

### 小程序中base64数据解码/编码示例
参考[小程序中base64数据解码/编码示例](https://opendocs.alipay.com/support/01rb0a)。 

### 字符串转换Hex String（十六进制字符串）
参考[字符串转换Hex String（十六进制字符串）](https://opendocs.alipay.com/support/01rb1w)。 

### 支付宝小程序内数组的排序问题（JS同理）
参考[支付宝小程序内数组的排序问题（JS 同理）](https://opendocs.alipay.com/support/01rb6t)。 

### 小程序定时器
由于平台限制，定时器 setTimeout 作用的代码在当前小程序切换到手机后台后不能正常执行，所以不能依赖定时器的确切时间，必须自己在回调函数中再次计算时间差；如需保证确切时间后做某些操作，请在服务器计时。
```javascript
const now = Date.now();setTimeout(()=>{  Date.now()-now // 可能 10000 也可能 20000},10000);
```

### JS 字符串中如何加入换行符号
**分析：**直接使用字符串数据进行axml渲染不支持\换行符，可以通过css来改变标签达到换行的目的；<br />**解决方案：**可以用css样式来控制换行，如：view的样式加上 white-space:pre-line 字符串数据的\就可以有效换行。<br />**自动换行：**word-wrap:break-word;<br />**超出显示省略号：**text-overflow:ellipsis;overflow:hidden;<br />其它用法可以自行搜索引擎搜索相关文章。 

### 小程序打开提示系统异常，调试面板没有报错
该错误一般由 page.json 文件里配置属性有问题导致的，可以去除一下相关内容测试判断是哪一块的问题。 

### 小程序里打印参数返回[Object,Object]如何处理
lo g打印数据时，直接显示[Object,Object]说明该参数是对象类型，请使用 JSON.stringify(参数名)转换成 JSON 字符串后打印。 

### new Date(2019-05-08 12:22).getTime() 加时间后Date取不到值
iOS 和 Android 存在兼容性，使用 getTime() 返回距 1970 年 1 月 1 日之间的毫秒数，可以使用写法：new Date("2019/05/08 12:22").getTime()。<br /> <br /> 
