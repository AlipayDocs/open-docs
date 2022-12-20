## Page()常见问题

### 监听页面返回事件
A 页面 B 到页面，然后返回 A 页面，监听页面返回事件可以通过以下方式实现：

- 可以通过 onBack 方法监听左上返回键。
- 通过页面 onshow 方法做页面的逻辑判断。 

### 如何获取小程序当前页面路径
[getCurrentPages](https://opendocs.alipay.com/mini/framework/getcurrentpages) ：JSON.stringify(getCurrentPages()[N].__proto__.route)，可以获取到页面路径（N 为页面数组栈中页面对象所在序号，最大值为当前页）。<br />**注意：**N 对应getCurrentPages().length-1。<br />[Page.route](https://opendocs.alipay.com/mini/framework/page-detail#Page.route)：Page 路径，对应 app.json 中配置的路径值，类型为 String。这是一个只读属性。<br />获取示例：
```json
//this指向当前Page,this.route即可获取到当前页面的路径值。
console.log(this.route)
```

## 小程序如何判断页面来源

- 小程序支持页面带参跳转，可以在跳转时加入自定义参数作为跳转标识，然后在被跳转页面中获取参数从而判断是从小程序中哪个页面跳转来的。<br />小程序页面带参数跳转：页面之间跳转 [my.navigateTo](https://opendocs.alipay.com/mini/api/zwi8gx) 可以直接在 URL 后拼接带参数跳转；从 page/index 的 onLoad 函数的 query 中读取 xx。

跳转示例：
```
my.navigateTo({url:'/page/index?xx=1'})
```

- [getCurrentPages](https://opendocs.alipay.com/mini/framework/getcurrentpages) ：JSON.stringify(getCurrentPages()[N].__proto__.route)，可以获取到页面路径（N 为页面数组栈中页面对象所在序号，最大值为当前页），既**N-1（对应getCurrentPages().length-2）**为上一页页面栈。

**注意：**如果跳转时使用的是关闭页面栈的方式，获取的路径不会是上一页，而是没有被销毁的上一个页面栈，因此不建议这样来判断。 

### 小程序上拉触底有什么API吗
小程序页面注册 Page() 的页面被拉到底部监听事件：[onReachBottom](https://opendocs.alipay.com/mini/framework/page-detail)。

### 小程序页面数据传递与接收
小程序上一页面数据传递，可在下一页面的onLoad方法中进行接收，详情参考 [小程序跳转](https://opendocs.alipay.com/support/01rb03)。 

### 小程序是否有页面栈深度限制
小程序建议将页面栈深度控制在10层以内。IoT 小程序也是一样。<br />可使用 [getCurrentPages](https://opendocs.alipay.com/mini/framework/getcurrentpages)方法查看当前页面栈数量。 

### 下拉刷新如何设置只开启当前页
参考[下拉刷新如何设置只开启当前页](https://opendocs.alipay.com/support/01rb7p)。 

### 小程序页面跳转传参，URL 长度限制
小程序本身对于页面跳转的 URL 不做任何限制，只受系统平台原生的限制，一般不建议超过 1K。 

### 获取页面栈某个页面的onload参数
无法获取非当前页面的 onload 参数，若参数需要跨页面操作可以尝试使用 [缓存](https://opendocs.alipay.com/mini/api/qm3ggk)。 

### 如何在页面JS生命周期回调函数中调用自定义方法
自定义方法定义在 Page()内，可以通过 this. 方法名 () 调用（this指向Page()）。<br />**注意：**有些时候是在调用某个API的回调函数中调用自定义方法，这时候 this 的指向有可能已经不是Page() ，会导致报错 'is not function' 可以在外层定义一个变量用来接收 this。<br />**例如：**
```javascript
onLoad(){let that=this;
         //在外层定义一个变量接收this(this指向Page())
         my.getOpenUserInfo({ success: (userinfo) => { 
           console.log(userinfo)that.viewTap();
         //调用自定义方法} 
        });
      },
       viewTap() {
       console.log('viewTap') },
```

- 自定义方法定义在Page()外,直接方法名() 调用。 

### 小程序页面关闭后重进数据依然保留了上次的赋值什么原因
通过设置 data 指定页面的初始数据。当 data 为对象时，被所有页面共享。即：当该页面回退后再次进入该页面时，会显示上次页面的数据，而非初始数据。这种情况，可以通过设置 data 为不可变数据或者变更 data 为页面独有数据两种方式来解决，详情可查看 [页面运行机制](https://opendocs.alipay.com/mini/framework/page-detail#%E9%A1%B5%E9%9D%A2%E6%95%B0%E6%8D%AE%E5%AF%B9%E8%B1%A1-data)。 

### Object.defineProperty 可以监听page.data 的数据变化吗
小程序中可以使用 Object.defineProperty 监听 JS 对象属性变化，但 Object.defineProperty 不可以监听 page.data 中数据属性的变化。<br />示例代码：
```javascript
let obj = {_hello:'hello world' //表示私有变量};          
           Object.defineProperty(obj,'hello',{get() {   
             console.log('get');     
             return this._hello;      
           },         
             set:function (value) {      
               console.log('set');      
               this._hello = value;       
             }\t\t\t\t\t});
console.log(obj.hello);
obj.hello = 'goodbye';
console.log(obj.hello);
```

### do not setdata with same object for path
这是 console 输出的警告，不是 error；表示 my.setData 的 data 数据和原来的 data 数据是同一份，数据无异常可以忽略。

### 调试报错：framework error: can not find page: pages/component/xxx/xxx
报错反馈内容指出，在小程序项目的“pages/component/view/view”路径中没有找到页面。<br />建议确认对应目录是否存在该页面，同时也可以查看开放文档中小程序框架的页面。 

## Page.json常见问题

### 设置小程序标题栏透明
参考[设置小程序标题栏透明](https://opendocs.alipay.com/support/01rb0y)。 

### 设置了onPullDownRefresh下拉刷新后真机测试没有效果

- 需要在对应页面的 .json 配置文件中配置 "pullRefresh":true 才能开启下拉刷新事件。
- app.json 的 window 属性里也可以配置 "pullRefresh":true 为全局设置。
- 需要在 onPullDownRefresh 函数里调用 my.stopPullDownRefresh 来停止刷新，否则会一直卡在下拉刷新事件里。
- app.json 里的 window 属性里 allowsBounceVertical 参数如果设置成 NO 也不能使用下拉刷新了。  
